# bia658-final-project
#final project

from TwitterSearch import *
import time,sys

file = open('result.txt','w')
dataset = set()
keyword = list()
keyword.append('iphone4')
keyword.append('iphone4s')
keyword.append('iphone5s')
keyword.append('iphone6s')

time.sleep(2)

def search(key):
	try:
	    tso = TwitterSearchOrder() # create a TwitterSearchOrder object
	    tso.set_keywords([key]) # let's define all words we would like to have a look for
	    tso.set_language('en') # we want to see German tweets only
	    tso.set_include_entities(False) # and don't give us all those entity information

	    time.sleep(2)
	    
	    # it's about time to create a TwitterSearch object with our secret tokens
	    ts = TwitterSearch(
	        consumer_key = 'x2Y9JOyk7QiJmfsb6KgsfKRkk',
	        consumer_secret = 'y1v1qZWhxEx2x4q6toIc8saY5KbWYcWEPukibey3V4yjqKmwwg',
	        access_token = '4041123441-Ybcn3wHtJb8W0ow5fRXAK0wSnO6wr0ck2dEWB2o',
	        access_token_secret = 'iIDVR4Gu92EsczxiIr0OmJl7goeGmxgLYexZ08iDYm8sN'
	     )

	     # this is where the fun actually starts :)
	    for tweet in ts.search_tweets_iterable(tso):
	        s = '@%s tweeted: %s' % ( tweet['user']['screen_name'].encode('utf-8').strip(), tweet['text'].encode('utf-8').strip() ) 
	        dataset.add(s+'\n')
	        if len(dataset) == 500:
	            for entry in dataset:
	                file.write(entry)
	        	break
	        	file.write('Key is end.\n')
	    time.sleep(2)

	except TwitterSearchException as e:
		print(e)    

for key in keyword:
	print 'Searching.. '+ key
	search(key)
file.close()

