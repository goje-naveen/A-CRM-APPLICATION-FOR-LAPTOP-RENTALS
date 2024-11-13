# CRM Application for Laptop Rentals

A robust and efficient CRM solution built using Salesforce, designed to streamline the process of renting laptops to customers. This application leverages Salesforce's powerful CRM capabilities to enhance customer interactions, optimize store operations, and improve overall efficiency.

## 🚀 Project Overview

The *CRM Application for Laptop Rentals* automates the management of inventory, customer information, booking processes, billing, and reporting. It provides a seamless experience for both users and administrators by integrating Salesforce Flows, Apex triggers, and custom objects.

### Key Features
- *Laptop Inventory Management*: Track and manage the inventory of laptops available for rent.
- *Customer Management*: Efficiently manage customer details, including contact information and interactions.
- *Booking Process*: Facilitate the entire lifecycle of laptop bookings, from request to fulfillment.
- *Automated Billing*: Streamline the billing process with automated invoicing.
- *User Roles & Profiles*: Define user roles such as Owners and Agents, with appropriate access levels.
- *Validation Rules*: Ensure data accuracy, such as phone numbers and email fields, using validation rules.
- *Automation with Flows & Apex*: Automate processes like laptop distribution and email notifications.
- *Reports & Dashboards*: Visualize data through reports and dashboards for actionable insights.

---

## 📋 Setup Instructions

Follow these steps to set up the project in your Salesforce environment:

### 1. *Create Custom Objects*
   - Navigate to *Setup* > *Object Manager*.
   - Create the following custom objects:
     - *Total Laptops*
     - *Consumer*
     - *Laptop Booking*
     - *Billing Process*

### 2. *Create Tabs*
   - Navigate to *Setup* > *Tabs*.
   - Create custom tabs for each of the custom objects.

### 3. *Create a Lightning App*
   - Navigate to *Setup* > *App Manager*.
   - Create a new Lightning app named *Laptop Rentals* and include navigation items for the custom objects.

### 4. *Create Validation Rules*
   - Navigate to *Setup* > *Object Manager* > *Consumer*.
   - Create a validation rule to ensure both phone number and email fields are not blank.

### 5. *Create Users*
   - Navigate to *Setup* > *Users*.
   - Create users with roles such as *Owner* and *Agent*.

---

## 🔄 Automation with Salesforce Flows

To automate the laptop distribution process, follow these steps:

1. Go to *Setup* > *Flows*.
2. Create a *Record-Triggered Flow* for the *Laptop Booking* object.
3. Set up conditions to check for laptop availability and assign laptops based on booking details.
4. Use an *Assignment* element to allocate laptops and an *Update Records* element to update the booking status.
5. Optionally, add an email alert to confirm bookings.

---

## 💻 Apex Development

### Apex Class: LaptopBookingHandler
The class handles email notifications when a booking is made:

apex
public class LaptopBookingHandler {
    public static void sendEmailNotification(List<Laptop_Bookings__c> lapList) {
        for (Laptop_Bookings__c lap : lapList) {
            Messaging.SingleEmailMessage email = new Messaging.SingleEmailMessage();
            email.setToAddresses(new List<String>{lap.Email__c});
            email.setSubject('Welcome to Laptop Rentals');
            String body = 'Dear ' + lap.Name + ',\n' +
                          'Thank you for renting with us! Your laptop details are as follows:\n' +
                          'Laptop Amount: ' + lap.Amount__c + '\n' +
                          'Core Type: ' + lap.core_type__c + '\n' +
                          'Laptop Type: ' + lap.Laptop_type__c;
            email.setPlainTextBody(body);
            Messaging.sendEmail(new List<Messaging.SingleEmailMessage>{email});
        }
    }
}


### Apex Trigger: LaptopBooking
This trigger sends email notifications after a booking is created or updated:

apex
trigger LaptopBooking on Laptop_Bookings__c (after insert, after update) {
    if (Trigger.isAfter && (Trigger.isInsert || Trigger.isUpdate)) {
        LaptopBookingHandler.sendEmailNotification(Trigger.new);
    }
}


---

## 📊 Reports and Dashboards

Generate reports and dashboards to visualize key metrics for the laptop rental business:

- *Reports*: Track booking status, customer interactions, and revenue.
- *Dashboards*: Get insights into inventory usage, customer satisfaction, and performance metrics.

---

## 🤝 Contributing

We welcome contributions! Feel free to submit a pull request or open an issue if you have suggestions or improvements.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 📞 Contact

For any questions or support, please contact the project maintainer.

---

This README covers all the key aspects of your project and provides comprehensive instructions for setting it up. Let me know if you'd like any additional sections or modifications!
