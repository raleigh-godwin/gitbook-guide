# Channel Manager Integration

Channel Manager Integration connects Mews Commander with external Channel Manager - an aggregator of booking engines all over the world. The main function of the connection between the Channel Manager and Mews Commander is to upload the availability and prices \(Mews Commander -&gt; Channel Manager -&gt; OTAs\) and to download reservations \(OTAs -&gt; Channel Manager -&gt; Mews Commander\).

The update of availability and prices works in two different modes

* Full update - when information for all connected room types and rates is sent \(can be triggered manually\).
* Delta update - when only difference from last delta update is sent \(can't be triggered manually\).

## Create

This is a general manual for creating any Channel Manager integration. If any concrete integration needs different approach, the approach is described in the section of the concrete integration.

1. Obtain a mapping codes for Room Types, Rates and Products and hotel's credentials.
2. Fill in the codes of Room Types and Products into proper row of Channel Manager Id property on settigns page.
3. Create the integration \(see [How to create integration](https://mewssystems.freshdesk.com/solution/integrations.md).\) but DO NOT ENABLE IT YET.
4. Fill in the Channel Manager Id of the hotel and Information email \(an email of the hotel \(usually reception\) to which notifications will be sent\) and other data if required.
5. Create Channel Manager Rates \(Make sure that none of the rates in Channel Manager are derived from another rate\).
   * Create new Channel Manager Rate by selecting an existing Mews rate and assigning proper mapping code.
   * Create Channel Manager Room Type for each mews room type that is connected with the rate. Note that the \_Room Type\_s should have mapping code already assigned. If you don't see some of the room types in the drop-down list it means the code wasn't set up in the room type description \(the same applies for Products\).
   * Create Channel Manager Product for each product that is always included in the rate \(Note that the \_Product\_s should have a mapping code already assigned\). See [Map Channel Manager Products](https://mewssystems.freshdesk.com/solution/articles/31000129946-channel-manager-integrations#how-to-map-channel-manager-products) for more details.
   * If the rate price will be supplied from Mews, leave IsSynchronzied ticked.
   * If the rate price will be calculated on Channel Manager, untick the IsSynchronzied \(the reservation delivery method will assign the rate properly\).
   * For more detail see [Map Channel Manager Rates](https://mewssystems.freshdesk.com/solution/articles/31000129946-channel-manager-integrations#how-to-map-channel-manager-rates)
6. Enable the integration
7. Enable the Upload prices and/or Upload availability operations and trigger Send inventory action manually for only a couple of days.
   * If the operation finishes with error or warning, it is probably because of mapping codes are set up incorectly. Check the mapping and run again. It may have failed because the connection is not activated yet on the side od Channel Manager - in this case you have to concact their support to enable the connection.
   * If the operation succeeds, you can continue.
8. Upload data for the whole period \(each channel manager accepts info for different number of days ti the future\).
9. Enable reservation delivery operation \(based on Channel maanager\) - see [Operations](https://mewssystems.freshdesk.com/solution/articles/31000129946-channel-manager-integrations#operations). Then trigger the Download reservations action if CHM allows to dowload old pending reservations \(from queue\).
10. Check that all reservations were downloaded and confirmed successfully. If not, deal with the errors somehow, until all reservations are downloaded and confirmed.
11. Enable the proper set of operations.
12. YOU CAN ENABLE THE INTEGRATION NOW.
13. Done. Congratulations.

> ### Mews Clues
>
> Please note that it is not possible to edit password information while the integration is enabled. You must first disable the integration, edit data as needed, and then re-enable it when all details are correctly entered.

## Map

**Map Rates**

There is several possibilities how a rate can be connected to channel manager via Channel Manager rate:

1. The rate exists in Mews and Channel Manager
2. the usual situation.
3. The rate exist only in Channel Manager
4. This helps when there is a special Channel Manager Rate set can't be achieved in Mews - e.g. some package rate.
5. Such Channel Manager Rate must be connected to rate in Mews to achieve proper reservation delivery.
6. There can be mmore such Channel Manager Rate connected to 1 rate in Mews.

Anyway the set up steps are:

* Create a new Channel Manager rate.
* Select proper Mews rate.
* Assign a proper mapping code.
* Set IsSynchronzied according to rate specification.

> ### Mews Clues
>
> * Please note that once charged product cannot be connected to a synchronized CHM rate \(via connecting it directly, or later modification\). In your stay product settings, you can change these preferences under the `Charging` field.

**Map Products**

From mapping you will obtain a code for each individual prouct or service, that is offered via CHM. Those codes need to be mapped in the product detail. If there is no code for any product specified in the CHM mapping, it usually means that the CHM just resends the code of the product from the OTA to Mews without change, so the OTA code of the product needs to be mapped instead.That is why the mapping field can hold multiple codes for multiple OTAs separated by;or by,.Those codes need to be obtained from each OTA - hotel should ask for it and finish the mapping.

\_Useful fact:\_The code for breakfast on Booking.com is usually1, so mapping the brakfast with code1will apply to Booking.com reservations. Providing such mapping will ensure, that all ordered services/products will be properly added to the reservation, when ordered by guest. Creating Channel Manager Product for Channel Manager Rate means: The product is always included in the rate. The cost of the product is added to the cost of the rate when the price is sent to CHM. The product is always added to the reservation eventhough the product/service was not ordered by guest.

## Manage

**Adding a new room type**

If hotels want to add a new room type to be sychronized with channel manager:

1. They need to obtain from the channel manager the mapping code for the room type and the rate codes the room type is connected to.
2. The room type mapping code should be set to the mapping property of the room type.
3. The room should be added to the list of connected room types on each channel manager rate \(on the integration detail\) the room type should be connected to.

**Removing a room type**

If hotel doesn't want to synchronize a room type anymore, follow these steps:

1. Remove the room type connection from all channel manager rates that connect the room type.
2. Remove the mapping code from the room type setting.

**Good to know**

If you would like to have a particular Room category bookable only by your hotel, you can exlude it from the mapping. The Channel manager integration will ignore that Room category, and you would be able to create reservations for it only internally.

## Operations

Every operation can be triggered either manually \(from the integration screen\) or by a background job that triggers the opertion on the integration \(if the integration has the operation enabled\). There are all operations that the integration might support:

* Create reservations
  * allows Mews Commander to create reservation from a direct input \(either manual or via API\).
* Ping notification
  * allows Channel Manager to ping Mews Commander, the reaction is to ask for reservations \(saves traffic\).
* Download Mappings
  * Mews Commader will ask for mapping information of the hotel. Result will be in a job logs.
* Download reservations
  * Mews Commander requests the Channel Manager for all pending reservations. After processing the reservations, Mews Commander confirms the reservations.
* Upload Availability
  * Mews Commander allows to send update of availability.
* Upload Rate Prices
  * Mews Commander allows to send prices and rate restrictions.

## Actions

To trigger operations on the integration manually, go to the integration detail page \(where the setting is\). On the bottom there is a form which enables to trigger some operations manually.Note that the operations run via jobs where only global admin has access. To check the status of operations, log in as a global admin in an incognito tab and check jobs \(the sign of an lightning\).

* Download Mappings
  * will create a background job that downloads hotel mapping from Channel Manager.
* Download Reservation
  * will create a background job that downloads pending reservations from Channel Manager.
* Send Inventory
  * will create a background job that uploads full update \(availability and/or prices\) for the specified period in the Channel Manager.
* Synchronization
  * will create a background job that triggers synchronization with the the Channel Manager.
* Create reservation
  * will create reservation based on data from Input field. Note that reservation will not be confirmed to Channel Manager.

## Troubleshoot

**Invalid mapping**

* When you receive an email with invalid mapping, it is crucial to fix the mapping as soon as possible. Because Mews disabled the integration, which means that until the mapping is fixed, no reservation will be downloaded and no availability/rate will be updated.

**Rates synchronization issues**

* If you receive a notification email that says something like rate update is not allowed, becaue updated rates are dependent \(linked, derived, ...\), you usually receive the rate code, so it is easy.
* In case this happens on AvailPro, you are not notified by an email, but by an angry customer, that complains that rates are not updated correctly. If synchronization doesn't help, you need to contact AvailPro, because they have mess in rate set up. There is some hidden rate dependency, and AvailPro needs to find it and give you the rate code.
* With the dependent rate code, you need to communicate with Channel Manager and Hotel to ask where the rate needs to be supplied from \(either from Mews or from Channel Manager and adjust mapping accordingly\).

**Reservations are not downloaded**

If hotel complains about reservation\(s\) not being downloaded, there could be a lot of reasons. Some of them:

* The integration is disabled or the Download Reservations or Ping Notificiation or Create Reservation method is disabled \(depends on channel manager which operation is used to obtain reservations\).
  * In this case enable the integraton/operation and wait for the job to get it \(if operation is

    Download Reservations\). Otherwise ask channel manager to resend the reservation.
* The resevation was downloaded, but hotel assigned it to another guest \(hotel just can't find it by the original guest name\) or updated it somehow. Just try to find it by channel manager code.
* The reservation wasn't sent to Mews \(accoring to logs\), but in Channel Manager is marked as delivered. In this case contact channel manager to get you the exact time of reservation download and confirmation number we send them as part of confirmation.
  * If they send you the data, check the logs again to see what happend.
  * If they don't have the data, means they didn't deliver the reservation an the problem is in channel manager.
  * In both cases the solution is to resend it from channel manager again.

**Disabling inventory push operations**

* When you need to disable the integration, so the availability and/or prices are not pushed to CHM, consier following information, before you disable just one of Upload Prices or Upload Availability operations. Laving just one of them enabled \(e.g. disable Upload Prices and leave Upload Availability enabled\) would cause trouble, because the periodical job will upload only "half" of data and will be marked as success, so the "other half" that was disabled from upload, will not be sent automatically and needs to be send manually.
* So you usually need to diable both of them.

