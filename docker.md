Copyright &copy; CAMMA, ICube, University of Strasbourg. All Rights Reserved.

<div>
<a href="https://cholectriplet2021.grand-challenge.org/">
<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/b/649/banner2022.x10.jpeg" align="left"/>
</a>
<br>
</div>

<br />
<br>

---------------------------------------------------------

Docker Build and Validation Guidedline
=========================================================

This guide provides 3-step processes to build and validate your Docker submission

1. Download host resources
2. Build Docker image
3. Validate Docker image

<br>

> ## 1.  Download Host Resources
- Download the CholecTriplet2022 host resources [here](https://seafile.unistra.fr/d/6331e913dc5d4318b258/)

- Extract the downloaded folder. The extracted folder will have the following structure:

```
    ───host/
        ├───input/
        |	  ├───data/
        |	  |	   ├───VID1.txt
        |	  |	   ├───VID2.txt
        |	  |	   ├───
        |	  |	   └───VIDN.txt
        |	  |
        |	  ├───record/
        |	  |	   ├───VID1/
        |	  |	   |	├───000001.png
        |	  |	   |	├───000002.png
        |	  |	   |	├───
        |	  |	   |	└───00000N.png
        |	  |	   |	
        |	  |	   ├───VID2/
        |	  |	   |	├───000001.png
        |	  |	   |	├───000002.png
        |	  |	   |	├───
        |	  |	   |	└───00000N.png
        |	  |	   |	
        |	  |	   ├───
        |	  |	   |
        |	  |	   └───VIDN/
        |	  |	   	    ├───000001.png
        |	  |	   	    ├───000002.png
        |	  |	   	    ├───
        |	  |	   	    └───00000N.png
        |	  |
        |	  └──gt/
        |	  	  ├───VID1.json
        |	  	  ├───VID2.json
        |	  	  ├───
        |	  	  └───VIDN.json
        |
        ├───output/
        |
        ├───validator/
        |     ├─── run.py
        |     ├─── eval.py
        |     ├─── triplet_to_id.json
        |     └─── timeout.py
        |
        ├───docker/
        |     └─── Dockerfile
        |
        ├───visualizer.py
        |
        └─── README.pdf

```

- Please, note the full path of your extracted download, let's call it `$HOST`, hence the subdirectory `input` is `$HOST/input`.

<br>

<details>
  <summary>  
  <big><b>Dataset visualization</b></big> (optional)
  </summary>

    Visualizing the data samples and annotations.

    % A. Use the following to see list of all available video IDs:
    
        cd $HOST
        python3 visualizer.py -l
    
    % B. To visualize the image and labels in a particular video:
    
        python3 visualizer.py -i --video videoID
    
    % C. Press Enter key to iterate over the frames.
</details>

<br>


> ## 2. Build Docker image

This section provides guide on how to transform your challenge method into a Docker image.

<br>

>> ### 2a. Docker preparation 
To build your Docker Image for method submission, you need the following:    
- (a). Dockerfile       
- (b). app


<br>

(a). **Dockerfile**: This is a file containing your Docker build definitions. This is the file that is compiled to create a Docker Image for your model. A template is provided here: `$HOST/docker/Dockerfile`. The information in the template is divided into 5 categories:
* (i) Installation libraries to run your code. Please add all dependencies that your model needs to run with here using the `RUN` keyword.
* (ii) Making sub-directories in your docker image to enable communication with the organizer's host drive
* (iii) Copying of your model into the Docker Image
* (iv) Specification of the code file to executed in order to run your model. In this case, you must specify the python file that runs your model in the `ENTRYPOINT`. 
* (v) Information about your team and system requirements as LABELs.

Please ensure your complete all TODOs in the template file.

<br>

(b). **app**: This is a single folder containing all your model code and weights/checkpoints. If your code needs to download any resources/weights online, please download and put inside this folder and modify your code to load those resources locally. Downloading from internet is not allow during model evaluation.


<br>


>> ### 2b. Structuring
With your modified `Dockerfile` and `app` directory, you can organize your submission as follows:

1. First, create a directory named `Team_submission` to contain all your submission files in the following structure:

```
Team_submission/
|- Dockerfile
|
|- app/
|   |- main.py
|   |- your_model.weights
|   |- your_model.code
|
|- input/
|- output/
```

2. Create two empty folders `input` and `output`.
3. Your actual code and checkpoints should be in the `app/` folder.


<br>

>> ### 2c. Build Docker
1. To build your Docker Image, you need an `image_name`. This must be the same as the LABEL for team in your Dockerfile.
2. Navigate to your submission folder:
```
    cd Team_submission
```
4. Build your docker as follows: 

```
    docker build -t <image_name> .
```
where:
- The -t flag allows you to specify a tag for the image you build. 
- <image_name> is the team name mention in (1) above.
- The `.` at the end of the command specifies that the Dockerfile to use is the in current working directory. Hence, make sure you are in the top level directory of the project where the `Dockerfile` is located.

Congratulations!, your have a Docker Image ready for submission, but wait, lets make sure it works. Let's test it...



<br>

> ## 3. Docker validation

Next is to test your Docker Image.
This section covers two **mandatory** testing protocol:

- (a). local testing
- (b). host testing

<br> 
Before the testing, let's understand the structure of the downloaded host resources.
The `$HOST` contains 4 directories: `input/, output/, validator/, docker/`:

<br>

**input/**
- *To be mounted with read only access during testing*

The `input/` sub-directory contains the validation dataset for Docker testing purpose.         
Please, note the full path to the downloaded `host` directory, which we earlier marked as $HOST, this means that the path to the `input/` sub-directory is `$HOST/input`.

The `$HOST/input/data` directory conatins N text files for N validation videos.         
Each line in these text files will correspond to the path to an image. Consecutive lines will correspond to temporally consecutive images. Your code will read images in the files, process them and produce outputs. All images will be in `PNG` format. This will be mounted in a read-only format. Please do not limit the number of text files or images that are expected from this folder! We will run sanity checks requiring additional file processing.         
The content of each text file `video_x.txt` is in the following format:

```
/path/to/image1.png
/path/to/image2.png
/path/to/image3.png
...
...
```
where image1, image2, image3, ... will be temporally sequential images. Note again that the challenge rules allow the use of only frames corresponding to preceding and current timesteps to make a prediction at a time.
 

<br>


**output/** 
- *To be mounted with read/write access*

This is where the model's output is written.         
For each of the above mentioned input text files: `video_x.txt`, the participant must make a corresponding json file `video_x.json` in the `$HOST/output` folder in the following content format

```
{
    frame_id:{
        "recognition": [probability of triplet 0,....probability of triplet 99],
        "detection": [
            {"triplet": triplet_id, "instrument": [tool_id, tool_prob,bbox_x, bbox_y, bbox_w, bbox_h]}
            ...
            {"triplet": triplet_id, "instrument": [tool_id, tool_prob,bbox_x, bbox_y, bbox_w, bbox_h]}
            ]
    }
    ...
    ...
}
```
where each frame id has the "recognition" and "detection" elements. The "recognition" contains a 100-length, indicating the probabilities of 100 types of triplets. The "detection" is a list of triplet instances, which have "triplet id", "instrument"'s location information. Please ensure that probability values being written are strictly between [0, 1].


<br>


>> ### 3a. Local testing
Here you test your docker locally to ensure it works as expected by running the following command:

```docker run --rm -v "$HOST/input:/input":ro -v "$HOST/output:/output":rw <image_name>```

- The --rm flag simply makes docker clean up after itself when it finishes executing.
- The -v flag allows you to specify a directory from your local machine to attach to the docker container for it to use. In this case, we want the docker container to have access to the test images in the host directory.    
During final testing, the organizer's drive will be mapped on this folder to allow your docker to read images.       
When your `input` and `output` folders are mapped to the organizer's host drive/directory, it will have access to all files within the organizer's sub-directories, and your docker structure will now look like this:

```
Team_submission/
|- Dockerfile
|
|- app/
|   |- main.py
|   |- your_model.weights
|   |- your_model.code
|
|- input/
|    |- data/
|    |   |- video_1.txt
|    |   |- video_2.txt
|    |   | ...
|    |
|    |- record/
|    |   |- video_1
|    |   |- video_2
|    |   | private.data
|    |   | ...
|    |
|    |
|- output/
```
- your docker container will read images from the host input folder.
- your docker container will write its output to the host output folder.
- <image_name> is the tag that you specified when running docker build previously.

**NB**: Apart from `input/` and `output/` directories, please, do not hard code the names of any other sub-directories in the organizer's `host`, they will likely change during the final evaluation.


<br>


>> ### 3b. Host testing
Here, you test your Docker submission using a `validator` system provided by the organizers. This helps you to debug any error in your Docker image. Your Docker image needs to pass this validation to be guaranteed to run in the organizer's host computer. At the end of your host testing, the validator produces a status file: `team_passed.log` which shows the failure/success of the Docker validation. This file must be uploaded on the challenge submission portal for the final Docker during submission.

To evaluate your Docker using the host validator, run the following command:
```
    cd $HOST
    python validator/run.py --tag_name <image_name>
```

At the end of each run, check the $HOST/output/ directory for the status and result of your validation. 
Errors (debug statements), results, and validation status will be provided in `eeror.log`, `results.log`, and `team_passed.log` files respectively. 
- On validation failed, debug and repeat docker build and validation (*Host testing*) until an error-free docker is produced.
- On successful validation, submit your Docker `team_passed.log` file to the challenge submission [portal](https://cholectriplet2022.grand-challenge.org/validation).


<br>

>>>>>>>>> Up Next: [Docker Submission](https://cholectriplet2022.grand-challenge.org/submission/) 

<br>

<br>

# Helpful hints
- Participants will be able to register as teams for the challenge. 
- Register your team via this [link](https://cholectriplet2022.grand-challenge.org/join)
- Each team will be able to participate and make a single submission for the challenge.
- The submission format will be based on docker images. 
- Although participants are advised to learn the basics of building and running docker images, no advanced docker expertise is required. 
- A quick start guide and tutorials to help you get started with docker is available [here](https://docs.docker.com/get-started)
- We provide 5 short video clips for the validation
- The test set used for official evaluation consists of 5 long laparoscopic cholecystectomy videos that are not public. This dataset will not be made available to the participants during the challenge.
- The docker validation phase will take place between June 1 and July 31, 2022. Your docker output at this stage is not considered for the final challenge evaluation. This is just a sanity check to ensure that your docker is compliant with our input/output (i/o) protocol.
- Any i/o error will be corrected by the participants within this period. It is important not to modify your docker template or code structure after the validation phase to avoid complications during challenge evaluation.
- Note that your model will be evaluated in an online mode meaning that we will simulate a real-time scenario during testing. To elaborate, while your model can leverage information from previous frames, it should not make use of future frames when predicting actions at the current timestep. Our testing i/o pipeline will check this.
- We expect your model to run on a single GPU
- Performance will be scored using Average Precision (AP), and  will be averaged over all frames over all videos. We may compare the method performances in different ways but only the stipulated metrics contained in the approved challenge proposal will be used in determining the challenge winners.
- We use the recommended [`ivtmetrics`](https://pypi.org/project/ivtmetrics) to evaluate the models for both recognition and detection. Please, ensure you pip install the latest version. `pip install ivtmetrics`

- We provide a simple working example using a random predictor model in our [colab code blog](https://colab.research.google.com/github/CAMMA-public/cholectriplet2022/blob/main/Getting_Started.ipynb)

- Some example code to help you get started with your Docker submission is also available [here](https://cholectriplet2022.grand-challenge.org/docker)

- Docker images are built based on the definition given in a Dockerfile. More information about defining Dockerfiles can be found [here](https://docs.docker.com/engine/reference/builder).

-----

*Please direct any questions you may have regarding docker and docker submission to the #docker-submission channel on the [T50 Challenge 2021 Slack channel](https://join.slack.com/t/t50challenge2022/shared_invite/zt-1a1ilne29-kuNl58zarZgRLZs_vXyigg)*




