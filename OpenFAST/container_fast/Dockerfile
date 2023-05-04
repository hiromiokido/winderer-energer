# Download latest Ubuntu base image
FROM ubuntu:latest

# Update software repo and install wget
RUN apt-get update && \
    apt-get install wget -y

# Download Anaconda or Miniconda (Miniconda is faster and less heavier)
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-py39_4.12.0-Linux-x86_64.sh 

# Install miniconda (you can use bash or not)
RUN bash Miniconda3-py39_4.12.0-Linux-x86_64.sh -b -p /home/miniconda3/
ENV PATH=/home/miniconda3/bin:$PATH 

# Activate base environment by default
RUN conda config --set auto_activate_base True

# Use conda to install openfast
RUN conda create -n openfast_env -y && \
    conda install -c conda-forge openfast -y

# Clone repo contents to the image
COPY . /home/wind-energy/

# Remove miniconda from the image
RUN rm ./Miniconda3-py39_4.12.0-Linux-x86_64.sh && \
    rm /home/wind-energy/Miniconda3-py39_4.12.0-Linux-x86_64.sh

# Define the working directory of the container
WORKDIR /home/wind-energy/openfast/

# Run python_teste.py
CMD ["python", "python_teste.py"]


# COMMENTS AND STUDY SECTION
#
# Once the code is written, open the VS CODE terminal and, once you are in the same path
#   as the Dockerfile, run 'docker build -t <your-container-name> . ' in the terminal.
#
# You can execute it in parts: test if the image is running correctly; install conda and 
#   set its environment; copy the repo and define the container working directory. Finally,
#   run the file of interest (python_teste.py). To test if it's working, run 'CMD [ "ls" ]'
#   below the command of interest. 
#
#
# If you want to install miniconda manually, I have already downloaded the file for you.
#   you can 'cd' to your parent directory instead, building the image from the parent 
#   directory, specifying the path to your Dockerfile:
#      docker build -t <some tag> -f <dir/dir/Dockerfile> .
#
# Copy the file to the specific path you want in the image (it must be in the same directory
#   you are - or you can use WORKDIR - but I decided to use the easiest path for now.)
#      COPY Miniconda3-py39_4.12.0-Linux-x86_64.sh .
#
# It will install the specified file in a new specified file (miniconda3) using -p
#      RUN  ./Miniconda3-py39_4.12.0-Linux-x86_64.sh -b -p /home/miniconda3/
#      ENV  PATH=/home/miniconda3/bin:$PATH 
#
# To remove the .sh file from your image:
#      RUN  rm ./Miniconda3-py39_4.12.0-Linux-x86_64.sh
#
#
# Version without my comments and explanations
#      FROM ubuntu:latest
#
#      RUN apt-get update && \
#          apt-get install wget -y && \
#          wget https://repo.anaconda.com/miniconda/Miniconda3-py39_4.12.0-Linux-x86_64.sh && \
#          bash Miniconda3-py39_4.12.0-Linux-x86_64.sh -b -p /home/miniconda3/
#
#      ENV PATH=/home/miniconda3/bin:$PATH 
#
#      RUN conda config --set auto_activate_base True && \
#          conda create -n openfast_env -y && \
#          conda install -c conda-forge openfast -y
#
#      COPY . /home/wind-energy/
#
#      RUN rm ./Miniconda3-py39_4.12.0-Linux-x86_64.sh && \
#          rm /home/wind-energy/Miniconda3-py39_4.12.0-Linux-x86_64.sh
#
#      WORKDIR /home/wind-energy/openfast/
#
#      CMD ["python", "python_teste.py"]
#