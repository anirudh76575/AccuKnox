# AccuKnox
Questions for Django Trainee at Accuknox 

Topic: Django Signals 

Question 1: By default are django signals executed synchronously or asynchronously? Please 
support your answer with a code snippet that conclusively proves your stance. The code does 
not need to be elegant and production ready, we just need to understand your logic. 


Answer:Django signals are executed synchronously by default in the same execution flow as the sender. The reciever function is executed immediately when the signal is sent.


#code snippet

from django.dispatch import Signal
import time

my_signal = Signal()

def my_receiver(sender, **kwargs):
    print("Signal received! Processing...")
    time.sleep(3) 
    print("Signal processing complete.")

my_signal.connect(my_receiver)

print("Emitting signal...")
my_signal.send(sender=None)
print("Signal emission complete.")



Question 2: Do django signals run in the same thread as the caller? Please support your 
answer with a code snippet that conclusively proves your stance. The code does not need to be 
elegant and production ready, we just need to understand your logic. 


Answer: Django signals run in the same thread as the sender by default.


#code snippet

from django.dispatch import Signal
import threading

my_signal = Signal()

def my_receiver(sender, **kwargs):
    print(f"Receiver running in thread: {threading.current_thread().name}")

my_signal.connect(my_receiver)

print(f"Signal sent from thread: {threading.current_thread().name}")
my_signal.send(sender=None)



Question 3: By default do django signals run in the same database transaction as the caller? 
Please support your answer with a code snippet that conclusively proves your stance. The code 
does not need to be elegant and production ready, we just need to understand your logic. 


Answer:By default, Django signals do not automatically run inside the same databasetransaction as the caller.


#code snippet
from django.db import models, transaction
from django.db.models.signals import post_save
from django.dispatch import receiver

class MyModel(models.Model):
    name = models.CharField(max_length=100)

@receiver(post_save, sender=MyModel)
def my_receiver(sender, instance, **kwargs):
    print("Signal received! Checking transaction status...")
    print("Inside transaction?", transaction.get_connection().in_atomic_block)

with transaction.atomic():
    obj = MyModel.objects.create(name="Test")
    print("Object created inside transaction.")





Topic: Custom Classes in Python 
Description: You are tasked with creating a Rectangle class with the following requirements: 
1. An instance of the Rectangle class requires length:int and width:int to be 
initialized. 
2. We can iterate over an instance of the Rectangle c****lass  
3. When an instance of the Rectangle class is iterated over, we first get its length in the 
format: {'length': <VALUE_OF_LENGTH>} followed by the width {width: 
<VALUE_OF_WIDTH>}



#code snippet

class Rectangle:
   def __init__(self, length: int, width: int):
        self.length = length
        self.width = width

   def __iter__(self):
        yield {"length": self.length}
        yield {"width": self.width}

rect = Rectangle(10, 5)
for i in rect:
    print(i)
