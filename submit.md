Copyright &copy; CAMMA, ICube, University of Strasbourg. All Rights Reserved.

<div>
<a href="https://cholectriplet2021.grand-challenge.org/">
<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/b/649/banner2022.x10.jpeg" align="left"/>
</a>
<br>

</div>

<br />
<br>

----------------------------------------------
CholecTriplet 2022 Docker Submission Guideline
==============================================

To submit your Docker for final evaluation, you need the following:
1. A successfully validated Docker Image
2. A success `team_name.log` status file produced by the validator on the Docker Image intended to submit.
3. You also need a `16-bit-tag_number`. You can generate one for your team using this [website](https://random.org/strings/). Instruction: enter 1 in random box and 16 in character boxand tick all checkbox, click `Get Strings`. Copy the generated 16-bit strings. Please remember that this number must never be changed after you have used it to submit your first Docker Image. Keep it save.
4. An `access token` to submit your docker on the organizer's docker-repo. This will be sent to your team. Please, contact the organizer's if you have not received it. Please make sure you register the dockerhub ahead.

<br>


## Tag Docker
Please follow the following specifications, to tag your Docker Image:

```
    docker tag <image_name> <docker_repo>/<image_name>_<16-bit-tag_number>
``` 
- The docker_repo is provided as : https://hub.docker.com/r/camma/cholectriplet2022

<br>


## Push Docker
You can push your docker to the DockerHub with the following command:
```
    docker push <docker_repo>/<image_name>_<16-bit-tag_number>

```
This will request the `access token` to complete.

After submitting your docker image, please proceed to submit your draft report and summary presentation on the challenge website.
These two files are needed to complete your challenge submission.

<br>



*Please direct any questions you may have regarding docker and docker submission to the #docker-submission channel on the [T50 Challenge 2021 Slack channel](https://join.slack.com/t/t50challenge2022/shared_invite/zt-1a1ilne29-kuNl58zarZgRLZs_vXyigg)*





