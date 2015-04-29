# Sentiment analysis with Pumpkin

The workflow contains three workers (seeds):
- `tweetinject.py` - reads a file with tweets and sends them to the queue
- `filter.py` - performs sentiment analysis on incoming tweets
- `collector.py` - counts tweets and writes result into a file

## Install missing dependencies if required

```
pip install pika
```

## Prepare *pumpkin* environment

You should copy required files to you VM (as it is explained in the assignment).

### Workers (seeds)

You should copy desired workers to `~/pmk-seeds` directory - or directory that you specify with `--taskdir` option (see below in section Run Pumpkin).

Do the following if you want to run all three workers on one VM:
```
scp *.py pumpkin:pmk-seeds/
```

### Classifier

Copy trained classifier to required directory.
```
mkdir -p /home/pumpkin/nltk_data/classifiers
```
```
scp movie_reviews_NaiveBayes.pickle pumpkin1:nltk_data/classifiers/
```

### Configuration file

Complete (see slides) and copy *pumpkin* configuration file into working directory
```
scp pumpkin.cfg pumpkin1:pumpkin/
```
You should also change a group name. With the same value for different groups, your workers might communicate with workers of other people since the messages are identified in the system by a pair: message type and a group.

## Run Pumpkin

In order to start pumpkin, execute:
Replace $taskdir by a chosen directory such as '~/pmk-seeds'
```
python DRHarness.py --supernode --taskdir $taskdir --broadcast --endpoints="tcp://*:*" --gonzales
```
## Prepare final result

Perform the computations as it is explained in the assignment. Then, you plot a graph that shows how the number of positive and negative tweets changes in time. First, if needed, sort the data:

```
sort --output=tweetstats.data tweetstats.data
```
and plot a graph (using gnuplot):
```
gnuplot plot.gnu
```
open the file `tweetstats.png`.
