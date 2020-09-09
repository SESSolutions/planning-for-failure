# planning-for-failure
Planning For Failure to Improve User Experience

## Unhappy Customer 1 
After the customer's click on submit button, the payment API did not return before 30s and hence the UI was not updated. However, the order was registered to the database and the payment was also processed successfully by payment API.

Assumption: The Rest API Post method that registers the order to the database may be in the same code block with the Payment API. This may be the reason why the order and payment are successfully processed even though the UI was not updated.  The UI was not updated because the Payment API did not return before 30s with the data to update UI.

### Unhappy Customer 2
The user would have clicked on the submit button twice and the payment API processed two payments, even though the order may have been registered once. Because of the sluggishness of the payment API and user's clicking on the submit button twice, the time interval for the payment API to return may be longer. However, the payment API might have returned for the first click, which made it look as if it returned faster for the second click.

Assumption: As mention in assumption 1, Rest API post method and Payment API may be in the same code block. Moreover, One order could be registered in the database because the order Id may be the same for the number of times the user clicked on the submit button, but the payment was processed twice because the user likely clicked on the button twice. Payment API did not return in time after the first click on the button and the user clicked again when he did not see any update on the UI. The payment API might have taken 45 second to return for the first click.

### Unhappy Customer 3
The user clicked on the button, but the UI was not updated because the payment API did not return with data to update UI; the user click on the button for the second time and the payment AP returned the data and the UI was updated. The user was charged twice because the payment API was processed twice. The reason is as mentioned above.

Assumption: Rest API post method and payment API may be in the same code block. The order Id is the same for the number of times the user clicked on the submit button, and hence the order was registered once in the database, but payment was processed twice. Payment API did not return in time after the first click and the user clicked again when he did not see any update on the UI. 

#### Solutions
To prevent users from clicking twice on the submit button, information may be displayed on the UI to inform the user that a payment for a placed order is being processed. In addition, the time that a payment API takes to return for a worst case may be displayed to the UI as the time it may take to process a payment of an order. Displaying a worst case estimated time would help the users not to click on the button more than necessary.

Another solution may be to disable the order submit button once user clicks on it, and order is registered, and payment is being processed. The order button would be enabled after the payment API returns for the click and the UI is updated.

A potential solution may be to have two-way binding and use the data that is coming from the UI to control the number of time payment API processes a payment. With such a data coming from the UI, the Rest API post method which may be in the same code block with Payment API can then be placed in a different code block with ‘if statement.’ 



