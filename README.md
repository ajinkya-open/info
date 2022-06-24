# info


from os import uname
from pydoc import cli
import paho.mqtt.client as mqtt
import time



under_test = {  
   	'1':'112771', 
	'2':'112778',
	'3':'112773',
	'4':'112774', 
	'5':'112777',
	'6':'112776', 
	'7':'112772', 
	'8':'112771' 
}


#     print("Connected with result code "+str(rc))

#     # Subscribing in on_connect() means that if we lose the connection and
#     # reconnect then subscriptions will be renewed.
#     client.subscribe("$SYS/#")

# # The callback for when a PUBLISH message is received from the server.
# def on_message(client, userdata, msg):
#     print(msg.topic+" "+str(msg.payload))

client = mqtt.Client()

#client.on_connect = on_connect
#client.on_message = on_message
client.will_set("device1/status", payload="Offline", qos=0, retain=True)
client.connect("broker.pongohome.in", 1883, 60)

# Blocking call that processes network traffic, dispatches callbacks and
# handles reconnecting.
# Other loop*() functions are available that give a threaded interface and a
# manual interface.
client.loop_start()

for j in range(1,500):
    print (j)

    for i in under_test:
        print(under_test[i])
        topic= under_test[i]
        client.publish('pushed','-->')
        client.publish(topic,'^[sync]')
        client.publish('pushed','======')
        time.sleep(5)


