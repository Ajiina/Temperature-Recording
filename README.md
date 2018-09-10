# Temperature-Recording
import RPi.GPIO as GPIO

import time

import dht11

import httplib, urllib

import time

GPIO.setmode(GPIO.BOARD)

GPIO.setwarnings(False)

t1 = dht11.DHT11(pin=3)



def txn(ser_id,data):
    
server_id=['field1','field2']
    
try:
        params = urllib.urlencode({server_id[ser_id-1]:data, 'key':'CQWLZMK8JIGVIIBA' }) 
   
     headers = {"Content-typZZe": "application/x-www-form-urlencoded","Accept": "text/plain"}
        
conn = httplib.HTTPConnection("api.thingspeak.com:80")
    
    conn.request("POST", "/update", params, headers)
      
  response = conn.getresponse()
       
 conn.close()
      
  print "Sent"
    
except:
       
 print "Sending Failed"


def dht1():
  
  t1_Result = t1.read()
 
   if t1_Result.is_valid():
      
  temp1= str(t1_Result.temperature)
      
  hum=str(t1_Result.humidity)
      
  txn(1,temp1)
 
 print temp1,hum
    
return temp1,hum

