# Define the Email class to represent an individual email.
class Email:
    def __init__(self, email_address, subject_line, email_content):
        # Initialize each email with sender address, subject, and content
        self.email_address = email_address
        self.subject_line = subject_line
        self.email_content = email_content
        self.has_been_read = False  # Track whether the email has been read

    # Mark the email as read by setting the flag to True
    def mark_as_read(self):
        self.has_been_read = True

# Global list to store all email objects
inbox = []

# Function to populate the inbox with sample emails for demonstration
def populate_inbox():
    sample_emails = [
        ("sender1@example.com", "Welcome to Our Service", "Thank you for joining us!"),
        ("sender2@example.com", "Your Subscription Details", "Here are your subscription details."),
        ("sender3@example.com", "Special Offer", "Check out our special offer!"),
    ]
    for email in sample_emails:
        inbox.append(Email(*email))

# Function to list all emails in the inbox with their read status
def list_emails():
    for index, email in enumerate(inbox):
        read_status = "Read" if email.has_been_read else "Unread"
        print(f"{index}: {email.subject_line} ({read_status})")

# Function to mark an email as read and display its content
def read_email(index):
    try:
        email = inbox[index]
        email.mark_as_read()
        print(f"\nEmail from {email.email_address}\nSubject: {email.subject_line}\n\n{email.email_content}\n")
        print("Email marked as read.\n")
    except IndexError:
        print("Invalid email index.")  # Handle invalid index access

# Function to display only unread emails
def view_unread_emails():
    print("\nUnread Emails:\n")
    for index, email in enumerate(inbox):
        if not email.has_been_read:
            print(f"{index}: {email.subject_line}")

# Function to get and validate user's choice
def get_user_choice():
    try:
        return int(input('''\nWould you like to:
    1. Read an email
    2. View unread emails
    3. Quit application

    Enter selection: '''))
    except ValueError:
        return None  # Return None if input is not an integer

populate_inbox()  # Populate the inbox with sample emails at program start

# Main program loop to interact with the user
while True:
    user_choice = get_user_choice()
    
    if user_choice == 1:
        list_emails()
        try:
            email_index = int(input("Enter the index of the email you want to read: "))
            read_email(email_index)
        except ValueError:
            print("Please enter a valid number.")  # Handle non-integer input
        
    elif user_choice == 2:
        view_unread_emails()  # Show unread emails only
                
    elif user_choice == 3:
        print("Quitting application.")  # Exit the program
        break
        
    else:
        print("Oops - incorrect input. Please enter 1, 2, or 3.")  # Handle invalid options
