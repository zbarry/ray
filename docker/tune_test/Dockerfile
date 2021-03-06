# The stress_test Docker image build a self-contained Ray instance for launching Ray.

FROM ray-project/base-deps

# We install ray and boto3 to enable the ray autoscaler as
# a test runner.
RUN pip install -U https://s3-us-west-2.amazonaws.com/ray-wheels/latest/ray-0.7.0.dev1-cp27-cp27mu-manylinux1_x86_64.whl boto3
# We install this after the latest wheels -- this should not override the latest wheels.
RUN apt-get install -y zlib1g-dev
RUN pip install gym[atari]==0.10.11 opencv-python-headless tensorflow lz4 keras pytest-timeout smart_open
RUN pip install --upgrade bayesian-optimization
RUN pip install --upgrade git+git://github.com/hyperopt/hyperopt.git
RUN pip install --upgrade sigopt
# RUN pip install --upgrade nevergrad
RUN pip install --upgrade scikit-optimize
RUN conda install pytorch-cpu torchvision-cpu -c pytorch

# RUN mkdir -p /root/.ssh/

# We port the source code in so that we run the most up-to-date stress tests.
ADD ray.tar /ray
ADD git-rev /ray/git-rev
RUN python /ray/python/ray/rllib/setup-rllib-dev.py --yes

WORKDIR /ray
