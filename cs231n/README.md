# Convolutional Neural Networks for Visual Recognition
* http://cs231n.stanford.edu/
* https://github.com/cs231n/cs231n.github.io/blob/master/google_cloud_tutorial.md
* https://cloud.google.com/sdk/docs/

# Potential Issues
### Importing matplotlib.pyplot
* pip install matplotlib

### No cs231n tarball for GCP instance
* https://www.reddit.com/r/cs231n/comments/93iyxa/cs231nrepodeepubuntutargz_not_found/

### Generate default jupyter notebook config file
* jupyter notebook --generate-config

### Can't install anaconda on instance with wget
* sudo apt-get install bzip2

### Can't open jupyter notebook from GCP instance
* gcloud compute ssh 'cv' --project='cs231n-230103' --zone='us-west1-b' --ssh-flag='-L' --ssh-flag='2222:localhost:8888'
