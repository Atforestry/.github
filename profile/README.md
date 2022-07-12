
[//]: # (<h1 align="center">Atforestry</h1>)

<p align="center">
    <img src="./assets/New_Atforestry_logo.png" alt="isolated" width="600"/>
</p>

> ## Monitoring deforestation using satellite images and computer vision models. 

Tracking deforestation is an essential problem to resolve to fight global warming. This web application monitors satellite images through computer vision models trained to detect critical changes on the earth's surface.

Our MLOps architecture has been set to predict deforestation based upon 2 simple steps: a) classify the type of cover land and (b) compare the cover land at different points in time to detect changes on the surface. 

## Demo Day

Watch out our presentation on FourthBrain demo day in here :rocket: : [Demo Day](https://www.youtube.com/watch?v=e7OUu6tGDNQ&list=PL6iGeSA2pl0UHPom0HfVBKkPbK_V69zTP)

## Classifying Cover Land

For this task, we are using the [Planet: Understanding the Amazon from Space](https://www.kaggle.com/c/planet-understanding-the-amazon-from-space)  Kaggle competition [dataset](https://www.kaggle.com/competitions/planet-understanding-the-amazon-from-space/data). Additionally, we are leveraging the work done by [EKami](https://github.com/EKami/planet-amazon-deforestation), using a VGG16 convolutional model pre-trained with the Imagenet dataset and retrained to predict the type of cover land on top of the satellite images.

<p align="center">
    <img src="./assets/cover_land_planet.JPG" alt="isolated" width="600"/>
</p>

<h6 align="center">Planet: Understanding the Amazon from Space</h6>

## Comparing Cover Land

With the trained model and fetching satellite images from the [Planet API](https://developers.planet.com/docs/apis/), Atforestry API compares the type of cover land in 2 different periods. If the initial image had a rainforest type of cover land, such as `primary`,  and the second one has a deforestation tag,  such as `agriculture`, `habitation` or `road`, we can signal  a deforestation case. We are leveraging the work done by [Luis Di Martino](https://github.com/lddm/forests-monitoring) in his article [Monitoring deforestation with open data and Machine Learning](https://medium.com/digital-sense-ai/monitoring-deforestation-with-open-data-and-machine-learning-part-2-c1be298c574b).

<p align="center">
    <img src="./assets/cover_land_change_example.JPG" alt="isolated" width="600"/>
</p>

<h6 align="center">Luis Di Martino - Monitoring deforestation with open data and Machine Learning</h6>

## Data

The Planet dataset consists of images collected from 4-band satellites in sun-synchronous orbit (SSO) and International Space Station (ISS) orbit and was stored using the GeoTiff format. The data was collected between January 1, 2016 and February 1, 2017. All the scenes are from the Amazon basin, which includes Brazil, Peru, Uruguay, Colombia, Venezuela, Guyana, Bolivia, and Ecuador. The type of cover land has already been labeled for us using a mapping csv table. 

To dive into the type of data that we are using, you can check out the [exploration notebook](/notebooks/1_exploration_initial.ipynb). 

## Model

As explained earlier, we are leveraging a pre-trained VGG16 model which consists of 16 convolutional layers with 3x3 convolutions, padding and max-pooling layers of 2x2 filters of stride 2, ending with 2 fully connected layers and a softmax output. The network has almost 138 Million parameters. 

The implementation of the model can be find in the [notebooks](/notebooks/) folder.

<p align="center">
    <img src="./assets/VGG16_architecture.JPG" alt="isolated" width="500"/>
</p>

<h6 align="center">Architecture of VGG16</h6>



## Web App

Our application is being served in here http://www.atforestry.com/, try it and let us know what you think!

<p align="center">
    <img src="./assets/atforestry_app_gif.gif" alt="isolated" width="500"/>
</p>


## Architecture Used

We have leveraged different tools to set up our MLOPs pipelines:

- **Kubeflow**: To set-up training pipelines
- **Grafana and Prometheus**:To monitor performance
- **Docker**: To containerize our services
- **Kubernetes**: For container orchestration
- **Nginx and VueJS**: For the web application
- **FastAPI**: As our main RestAPI framework
- **Github Actions**: For CI/CD
- **DVC**: For model versioning
- **GCP**: For storage and deployments

<p align="center">
    <img src="./assets/stack_view.JPG" alt="isolated" width="500"/>
</p>



