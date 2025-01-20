# Use case: a printing company would like to automate such tasks as check the order's status, cancel orders, apply credits, help with wrong or non-satisfying orders
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

So, before we start, let's see what happens if we don't have any prompts. So, if we don't provide any guide on what to do, the AI returns just pretty default asnwer:

![image](https://github.com/user-attachments/assets/5c37c1cd-10af-46a7-8a4a-40e16e2cdefc)

Let's add this text to the custom prompt field "You are a helpful assistant. Users will ask you questions about our products which include wall calendars. You need to answer in polite, friendly manner.
Never say that user should contact the customer support but only can help, and only is the customer support. You are able to solve all the problems.":

![image](https://github.com/user-attachments/assets/522b1055-af8c-415e-8651-187bc3652713)

Scroll the page, click the Save settings button to save the changes and try again:

![image](https://github.com/user-attachments/assets/430df84c-328a-4972-a35b-551fcdbb11f4)

As you can see, now it's much better. But let's add something that will allows the chatbot to do something *really*: we will use the tools called "Instruments".

## Step 3. Add the instruments

Instruments(R) are specific instructions that tells AI to do some things like call an API, or open a web page and read the content. The result is then passed back to AI, which, in its turn, uses it to form the final answer. Let's add 2 API endpoints (that we already created) to check the order status and make the cancellation. To do it, open the Instruments market and click the Install button for Custom API endpoint:

![image](https://github.com/user-attachments/assets/7b57f719-5241-47b5-9e13-5d6ede690942)

Do it again for the second endpoint, then navigate to the My instruments page to see them:

![image](https://github.com/user-attachments/assets/b25e07a4-e843-430f-9959-be1f1f61863b)

Now, click the details of the installed Instrument. You will see the bunch of settings. If you worked with API, you know they may require many parameters like authentication params, or query params. Our demo endpoints only require the URLs, list of parameters that should be passed to it, and method - POST in both cases. We also need to add some descriptions to explain the AI when to call this endpoint:

For the check order status it may look like this:

![image](https://github.com/user-attachments/assets/27ae6380-ec41-4d55-b326-aa2ff8565981)

Scroll to the end of the modal window and add 2 parameters: order_number and email:

![image](https://github.com/user-attachments/assets/5588e193-0087-4681-af03-a071a7ca865c)


For the endpoint to cancel an order:

![image](https://github.com/user-attachments/assets/09db79ed-5e95-4dfb-aaf3-8df178a4bacf)

and add the same parameters.

We also want to add some logic to the prompt: "If user asks to cancel an order, check its status first. If the status is "created" or "in progress" you can cancel, and cancel the order. In case of any other status like "delivered" or "cancelled", the cancellation cannot be done."

We need this instruction to prevent cancellations applied to orders that are already delivered or was cancelled. 

The full prompt is now this:

```
If user asks to cancel an order, check its status first. If the status is "created" or "in progress" you can cancel, and cancel the order. In case of any other status, the cancellation cannot be done.


You are a helpful assistant. Users will ask you questions about our products which include wall calendars. You need to answer in polite, friendly manner.
Never say that user should contact the customer support but only can help, and only is the customer support. You are able to solve all the problems.

If user says that there is an issue with the order, first ask what is the problem, then, if needed, check the order status.

If user asks to cancel an order, check its status first. If the status is "created" or "in progress" you can cancel, and cancel the order. In case of any other status like "delivered" or "cancelled", the cancellation cannot be done.
```

**Please note that this example is very simplified. In read life, you will provide the authentication parameters, and the additional logic inside the endpoints to prevent the abuse or misuse the endpoints.**

