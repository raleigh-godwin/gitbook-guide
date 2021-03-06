# Review and Invoice

An invoice as a list of bill items that will not be paid at the time of checkout, but will have a future date of payment. From the moment that an invoice is issued, it is considered a legal document and cannot be amended.

{% hint style="info" %}
### Mews Clues {#mews-clues}

Please note that you cannot modify the address or name on a bill once it has been closed. Furthermore, altering any information within the customer or company profile will not affect closed bills in any way. If you need to fix the name or address on a closed bill, you can rebate the bill using the Rebate button and issue a new bill once the customer or company details have been amended.
{% endhint %}

## Settings

There are a few settings that directly apply to invoicing, which can all be found in your `Accounting configuration`.

Within the `Options` field, we would recommend selecting `Receivable tracking enabled`. This will allow you to track payments for outstanding invoices and their respective due dates. You can find this information in the [`Bills and Invoices`](https://mews-systems.gitbook.io/guide/commander/reports/bills-and-invoices) report.

Secondly, you must also check that invoicing is enabled. Within the `Enabled external payment types` field, be sure that you have selected `Invoice`, along with any other payment types that you'd like to use at your property.

In these settings, you can select a `Default invoice counter`. This field is a drop-down menu of all counters being used at your property. Choose a counter that will be pre-filled for all future invoices, or alternatively, some properties choose to create a counter used only for invoicing. Please note that this field can be edited before invoices are issued.

**Invoice due interval**

Lastly, you will find a field titled `Invoice payment`, where you can select an accounting category dedicated only to receiveable invoice payments.

For more information about `Accounting Configuration` options, [`click here`](https://mews-systems.gitbook.io/guide/commander/settings/finance-settings/accounting-configuration).

## Issue

To issue an invoice, navigate to the customer profile `Billing` screen of the guest. When ready to issue, move all `Unpaid items` to the `Open bill` of the customer, look for the `Issue invoice` button at the bottom of that section, and click on it.

A new window will appear, where you will see a full summary of all items included in the invoice. For a more detailed description of item details, please see below. You will also see the following fields to complete:

* **Customer** - Pre-filled with customer name
* **Printer** - If you'd like to print the invoice, select which printer you'd like to use. If a printer is selected, the document will print automatically when you click `Issue invoice`.
* **Bill Counter** - Select the bill counter that you'd like to use to close this bill.
* **Fiscal registry** - Select the correct fiscal registry integration that your accounting team is using.
* **Fiscal machine** - 
* **Due date** - Date that payment should be received by
* **Unique identifier** - Any identifying number provided by your accounting software.
* **Informative Currency** - Select the guest's preferred currency to display the balance for their own information. Please note that payment must still be taken in the property's local or chosen currency. If no currency is selected, your default currency will be used.
* **Address** - Customer's billing address, pre-filled with the address from the customer's profile. If different, search for the billing address in the `Google address bar` and select to automatically fill address details. This will be editable after the bill is closed. 
* **Notes** - Add any additional notes or information. This will be editable after the bill is closed.

Below these fields, you will find the `Issue invoice` button. If all information has been reviewed and is correct, click on this button.

This invoice is now successfully closed and you will be automatically redirected to the final closed invoice.

## Items

A complete list of each bill item is always included in issued invoices. Items may include stay services as well as any products or additional services that the customer may have ordered.

Bill items are expandable and collapsible using the `+` and `-` buttons, however when the invoice is printed or exported as a document, all items are fully listed in their expanded form.

Stay items include the following information on each line:

* **Reservation number** - Unique number generated by Mews and connected to the reservation
* **Channel confirmation ID** - Optional number entered at time of booking creation
* **Customer** - Name of customer who made the reservation
* **Dates of stay** - Date of arrival and date of departure
* **Room category** - Room category used for duration of stay. Requested category may not be listed here.
* **Room number** - Space used for the duration of stay.

All items, including stay items, are listed with the following details:

* **Bill item** - Name of bill item according to property settings. Click on this title to be view reservation or order details for any item.
* **Created** - Date and time that item was created in system.
* **Tax rate** - Correct tax percentage for each item
* **Net** - Cost of item, excluding tax
* **VAT** - Tax alone, excluding item cost
* **Value** - Total cost, including tax and item cost
* **Totals** - Total sum listed under each respective column

{% hint style="info" %}
### Mews Clues

If some of these fields are not visible, the information may be collapsed. Click on the `+` and `-` buttons to see more or less.
{% endhint %}

Below the bill item summary, you will see a summary of all received payments, displayed with the following details:

* **Payment** - Payment type and card details, if applicable
* **Created** - Date and time that payment was created
* **Value** - Amount paid including the respective currency symbols
* **Totals** - Total sum of payments listed under the `Value` column

At the very bottom of the `Review and invoice` page, you will see `To be paid`, which states a total balance owed including value and currency.

{% hint style="info" %}
### Mews Clues

In case of a negative amount, the bottom section will read `To be refunded` instead of `To be paid`.
{% endhint %}

## Receivable Payments

When you return to the billing page of that customer, you will find a separate bill item in the `Unpaid items` section for each issued invoice. Item will be labeled `Receivable invoice payment` listed with the corresponding invoice number.

Move this item to the customer's `Open bill`, transfer the item to another bill, or assign to a company. When ready, accept payment as normal and you will be able to review and close this item on a new bill.

