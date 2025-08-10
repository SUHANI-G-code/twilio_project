WhatsApp Message Scheduler using Twilio and Python
Features--
 1.Import the Twilio library
 2.Create a function to send WhatsApp messages
 3.Take user input for recipient and message
 4.Schedule messages for a specific date and time
 5.Send the message automatically at the scheduled time
 Requirements--
 1.Python 3.x
 2.twilio library (pip install twilio)
 USASGE-
 from twilio.rest import Client
from datetime import datetime
import time

# Twilio credentials
account_sid = "AC00bed49775fe5b10c4228d0cc8f9efac"
auth_token = "27b37071671e5a2f1070b0c06c2e5c9e"

client = Client(account_sid, auth_token)

# Function to send WhatsApp message
def send_whatsapp_message(recipient_number, message_body):
    try:
        message = client.messages.create(
            from_ = "whatsapp:+14155238886",
            body = message_body,
            to = f"whatsapp:{recipient_number}"
        )
        print(f"Message sent successfully to {recipient_number}")
    except Exception as e:
        print(f"Failed to send message to {recipient_number}. Error: {e}")

# User input
name = input("Enter recipient name: ")
recipient_number = input("Enter recipient number with country code: ")
message_body = input("Enter message body: ")

# Scheduling message
date_str = input("Enter date of the message (YYYY-MM-DD): ")
time_str = input("Enter the time of your message (HH:MM): ")

scheduled_time = datetime.strptime(f"{date_str} {time_str}", "%Y-%m-%d %H:%M")
current_time = datetime.now()

# Calculate delay
time_difference = (scheduled_time - current_time)
delay_time = time_difference.total_seconds()

if delay_time > 0:
    print(f"Message will be sent after the delay time to {name} at {scheduled_time}")
    time.sleep(delay_time)
    send_whatsapp_message(recipient_number, message_body)
else:
    print("The scheduled time is in the past. Please enter a valid time.")

##NOTE
Make sure your Twilio account is set up for WhatsApp messaging.
If using the Twilio sandbox, the recipient must join the sandbox first.
All phone numbers must include the country code (e.g., +91...).
