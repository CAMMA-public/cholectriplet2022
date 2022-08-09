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
2. A success `team_name.log` status file produced by the validator on the Docker Image you intended to submit.
3. A string of `8-bit-tag_number`. 
4. An `access-token` to submit your Docker Image on the CholecTriplet docker-repo. 

<br>

**NB**: The `8-bit-tag_number` and `access-token` will be sent to your team. Please, contact the organizer's if you have not received them. 

<br>
<hr>
<br>

## 1. Submit Docker Validation Report
You final submission docker must be self-validated using the host-validator provided by the organizer at validation phase. 
This ensures that docker is in compliance with the organizer's evaluation pipeline.

>> * Validation Log: [click to upload](https://seafile.unistra.fr/u/d/7d934b7f5a6b4d3ca92f/)
 
In case of any changes/update on the final docker, a re-validation is required.

<br>
<hr>
<br>

## 2.    Tag Docker
Please follow the following specifications, to tag your Docker Image for final submision:

```
    docker tag <image_name> <docker_repo>/<image_name>_<8-bit-tag_number>
``` 
- The `docker_repo` to be used is : https://hub.docker.com/r/camma/cholectriplet2022


<br>
<br>


## 3. Push Docker
Then, push your docker to the DockerHub with the following commands:
```
    docker push <docker_repo>/<image_name>_<8-bit-tag_number>

```
This will request the `access-token` to complete.

<br>
<hr>
<br>


## 4. Submit Draft Report
A summary of the proposed method is required to complete your challenge submission. Please ensure you use the provided template and complete all fields marked required (*).

>> * Method Report: [click to upload](https://seafile.unistra.fr/u/d/6b6f3271ac8a42aaa9fc/)


<br>
<br>

## 5. Submit Summary Presentation
A one-minute slide/video presentation of your proposed model is needed to complete your challenge submission. This will be used to present your method at MICCAI in Singapore.

>> * Presentation: [click to upload](https://seafile.unistra.fr/u/d/0ec9d916a90c455db81e/)



<br>
<hr>
<br>






*Please direct any questions you may have regarding docker and docker submission to the #docker-submission channel on the [T50 Challenge 2022 Slack channel](https://join.slack.com/t/t50challenge2022/shared_invite/zt-1a1ilne29-kuNl58zarZgRLZs_vXyigg)*





