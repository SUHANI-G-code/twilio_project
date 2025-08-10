import the twilio library,
create a function to send a message,
user input,
scheduling message,
send message.
from twilio.rest import Client
from datetime import datetime, timedelta
import time
# client crendentials
account_sid="AC00bed49775fe5b10c4228d0cc8f9efac"
auth_token="27b37071671e5a2f1070b0c06c2e5c9e"

client=Client(account_sid,auth_token)

#desgin the message
def send_whatsapp_message(recepient_number,message_body):
    try:
        message = client.messages.create(
            from_ = "whatsapp:+14155238886",
            body = message_body,
            to =f"whatsapp:{recepient_number}"
        )
        print(f"message sent successfully to {recepient_number}")
    except Exception as e:
        print(f"failed to send message to {recepient_number}.error:{e}")

#user input
name=input("enter recepient name: ")
recepient_number= input("enter recepient number with country code:")
message_body=input("enter message body: ")

#scheduling message
date_str= input("enter date of the message (YYYY-MM-DD): ")
time_str=input("enter the time of your message (HH:MM):")


scheducled_time = datetime.strptime(f"{date_str} {time_str}","%Y-%m-%d %H:%M")
current_time = datetime.now()

#CALCULATE DELAY
time_difference = (scheducled_time -current_time)
delay_time= time_difference.total_seconds()

if delay_time >0:
    print(f"message will be sent after the delay time to {name} at {scheducled_time}")
    #wait for the scheduled time
    time.sleep(delay_time)
    #send message
    send_whatsapp_message(recepient_number,message_body)

else:
    print(input("the scheducled time is in past please enter a valid time: "))

    
