# MICCAI Reproducibility Checklist

This checklist is aimed at facilitating reproducible research within the Medical Image Computing & Computer Assisted Intervention (MICCAI) conferences. Following similar efforts at Machine Learning and Computer Vision Conferences, we propose the implementation of the following guidelines for the submission of papers to the MICCAI conference.

---

This checklist is aimed at machine learning research in the medical image computing / analysis domain, and may not be directly applicable for CAI research.

We would like to start a discussion in the community and enable incremental improvement of this initial version compiled during the MICCAI 2020 hackathon. We hope to receive your pull requests and suggestions to put together a broadly supported version.


## Code availability

*   Provide links to the complete code used for the study
*   Provide ReadMe instructions and informations on parameter settings
*   Specify dependencies


## Model availability

*   Make pre-trained model available
*   Provide a container (e.g., Docker, Singularity) with instructions (see below)


## Containerization (e.g., Docker, Singularity)

The code and model can be containerized in a Docker. Docker containerization is used to simplify the deployment of applications. Specifically, docker containerization is used to “wrap” your entire application (including all dependencies and the operating system) into a single container. This container can be run as if it would be a single standalone application, anywhere, on any platform. Because the method and all dependencies are included in the container, the method is guaranteed to run exactly the same all the time.


* Data Access: how could you map the test data into the docker

  Because your container runs in an isolated environment, the data needs to be mapped into the container. The input data will be mapped into /input, read-only. The output of the method needs to be written into /output.

* Run the test example: python train.py

* Run the evaluation: python eval.py

* Docker Command: an example for segmentation application:

  *   _CONTAINERID=`docker run -dit -v [TEST-DIR]:/input:ro -v /output docker_application_name`_
  *   `_docker exec $CONTAINERID python train.py_`
  *   `_docker exec $CONTAINERID python eval.py_`
  *   `_docker cp $CONTAINERID:/output /local/path/output/saveresult_`
  *   `_docker stop $CONTAINERID_`
  *   `_docker rm -v $CONTAINERID_`

* Example for building a Docker for segmentation:

  *   [https://github.com/zengguodong/IVDM3SegChallenge](https://github.com/zengguodong/IVDM3SegChallenge) 
  *   A detailed description of the python example is provided here: [https://ivdm3seg.weebly.com/methods.html](https://ivdm3seg.weebly.com/methods.html).


## Experiment Design

*   Describe how to do the splits of dataset into the train / validation / test (e.g., N-fold cross-validation). Include the distribution of relevant parameters across splits.
*   Describe the algorithm / model used
*   Describe the tested hyper-parameter ranges and all relevant settings
*   Include information on the sensitivity regarding parameter changes
*   State any assumptions
*   Describe results with central tendency and variation.


## Data reporting

*   Thoroughly describe the study population. Include the following points:
    *   Is my study population representative for the full range of expected variability?
    *   Report on any deviations from the general expected patient population
*   All relevant statistics, such as number of samples
*   Clearly state inclusion and exclusion criteria, and how that influenced your sample size
*   If possible: Make data available. If not, try to include publicly available “toy example” data such that your code can be run.
*   Report image acquisition parameters for the data you used to train and evaluate your method. This ensures an assessment is possible if the method / model is applicable to e.g., data from a different center.


## Reporting of clinical problems

*   Include information on the clinically relevant range of parameters.
*   If possible, include information on clinically relevant performance. E.g., for segmentation while technically challenging, a clinician may not profit from a DICE increase of 1%, but from a more robust approach.

This checklist was heavily inspired by [https://www.cs.mcgill.ca/~jpineau/ReproducibilityChecklist.pdf](https://www.cs.mcgill.ca/~jpineau/ReproducibilityChecklist.pdf)
