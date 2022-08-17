Copyright &copy; CAMMA, ICube, University of Strasbourg. All Rights Reserved.

<div>
<a href="https://cholectriplet2021.grand-challenge.org/">
<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/b/649/banner2022.x10.jpeg" align="left"/>
</a>
<br>

</div>

<br />
<br>
<br>

----------------------------------------------
CholecTriplet 2022 Docker Submission Guideline
==============================================


## Requirements

To submit your Docker for final evaluation, you need the following:
1. A successfully validated Docker Image. 
2. A success `image-name_passed.log` status file produced by the validator on the Docker Image you intended to submit.
3. Private keys (`team-key` and `access-token`) to submit your Docker Image on the CholecTriplet DockerHub. 


<br>

**NB**: The private keys will be emailed to your team, do not compromise it and do not share with anyone outside your team.
Please, contact the organizer's if you have not received them.

<br>
<hr>
<br>



## 1. Submit Docker Validation Report
You final submission docker must be self-validated using the host-validator provided by the organizer at [validation phase](docker.md). 
This ensures that docker is in compliance with the organizer's evaluation pipeline.

>> * Validation Log: [click to upload](https://seafile.unistra.fr/u/d/7d934b7f5a6b4d3ca92f/)
 
In case of any changes/update on the final docker, a re-validation is required!

<br>
<hr>
<br>



## 2.    Access the DockerHub Submission Repository
Login to the Challenge DockerHub using the following command:

```
    docker login -u <team-key>
``` 
 **Password:** This will request your private `access-token` to complete.


<br>
<br>



## 2.    Tag Docker
Tag your Docker Image for final submision using the following format:

```
    docker tag <image-name> <team-key>/submission/<image-name>:latest
``` 
 - Example: if your Docker _image-name_ is "team-endovis" and your private _team-key_ is "endovis22", tag your Docker as follows:
```
    docker tag team-endovis endovis22/submission/team-endovis:latest
``` 


<br>
<br>




## 3. Push Docker
Then, push your docker to the DockerHub with the following commands:
```
    docker push <team-key>/submission/<image-name>:latest

```

<br>
<hr>
<br>


## 4. Submit Draft Report
A summary of the proposed method is required to complete your challenge submission. This will help to understand your proposed method and also contribute in writing a joint publication manuscript of the challenge methods. Please ensure you use the provided [template](https://seafile.unistra.fr/f/f7d626afa2d2433fa8a4/?dl=1) and complete all fields marked required (*).

>> * Method Report: [click to upload](https://seafile.unistra.fr/u/d/6b6f3271ac8a42aaa9fc/)


<br>
<br>

## 5. Submit Summary Presentation
A one-minute slide/video presentation of your proposed model is needed to complete your challenge submission. This will be used to present your method at MICCAI in Singapore. Please, use this [template](https://seafile.unistra.fr/f/31dd2c2a9876475a9687/?dl=1).

>> * Presentation: [click to upload](https://seafile.unistra.fr/u/d/0ec9d916a90c455db81e/)

_Optionally, you can also submit a transcript of your video._

<br>
<hr>
<br>






*Please direct any questions you may have regarding docker and docker submission to the #docker-submission channel on the [T50 Challenge 2022 Slack channel](https://join.slack.com/t/t50challenge2022/shared_invite/zt-1a1ilne29-kuNl58zarZgRLZs_vXyigg)*





