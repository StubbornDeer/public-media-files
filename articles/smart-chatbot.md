In this article, we review how to create a smart and helpful chatbot that not only answers users' questions but also calls API to make some actions and reads from the Internet to obtain the needed information.

## Step 1. Create a project with a text data source
Let's start with creating a project and adding a simple data source to start.

### Navigate to the projects list

![image](https://github.com/user-attachments/assets/dbc76673-2227-4f69-8c8c-590b444d5835)


Click the "Add a project" button and enter the project name:

![image](https://github.com/user-attachments/assets/30b2dd54-70f8-4602-9ab7-afa6587d5228)

Navigate to the data source and click the "Add a data source":

![image](https://github.com/user-attachments/assets/e6ca3452-d49b-4fb7-8e4f-600ae943de6c)

Select the "Plain text" from the list and click the "Add this source" button:

![image](https://github.com/user-attachments/assets/cd144df4-0432-441a-86ef-cc943382d5c3)

Click the "Add text content" button and enter the title and text content into the modal window:

![image](https://github.com/user-attachments/assets/cd14add6-d7a8-428c-b52e-556ab42b27e6)

Then click the "Save and index" button to save the text and index it to make available for the chatbot:

![image](https://github.com/user-attachments/assets/728a9d9f-68d0-4348-bb49-6b128ca617f8)

Now, let's conduct a simple test to see if the chatbot already picks up the content. Open the interaction window - this is where we will test our chatbot.

![image](https://github.com/user-attachments/assets/6c0dbfec-c010-4198-b77d-4355087a68b0)

Click the "Chat" panel and enter a question in the text area below, then click the button to send it. As we can see, the chatbot replies pretty nicely:

![image](https://github.com/user-attachments/assets/3b148891-7f0b-4a04-84af-7563eeeb5f11)

## Step 2. Add the custom prompt.

But what if we want the chatbot to do something more complicated, say, check the order status, apply the credits to an account, or even cancel the order? To achieve it, we have to provide the chatbot with the corresponding instructions. We can do it using 2 tools in the Enum:

1. Custom prompt
2. Instruments(R)

In a custom prompt, we add the instructions that will tell the chatbot how to behave. For example, we can tell it:

- which data to collect
- what to do if some condition is met or not met
- and what not not do.

