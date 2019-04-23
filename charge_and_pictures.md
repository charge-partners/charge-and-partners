# Charge&Pictures

You want to have more content for your charging locations? Charge&Pictures is there to help you.
You provide us with your location data (geo position and location IDs); we take care to build up content for those locations and deliver it to you with a set of APIs.

## Service setup

To use this service, all you need to do is deliver us your charging locations by using the [update location mappings](update_location_mappings.md) endpoint:


## Using the picture service

Now that we can match our picture database with your location identifiers, you can use one of our API methods to retrieve those pictures and present them to your users.
Please do not download the pictures and host them yourself; we make sure to provide the content with a good performance and high availablity (using location based routing and caching and a highly redundant content delivery network).
You can of course cache the links to the pictures per location; just ensure to refresh your cache on a daily basis to keep your cache up to date.

The following APIs are available to you:

- [get pictures by location](get_pictures_by_location.md)
- [get location details](get_location_details.md)
- [add picture to location](add_picture_to_location.md)

## Some background information 
There are a few things to keep in mind when using this service.
We generate the input by providing challenges to our users and rewarding their input. Thus the data is retrieved in a community based process.
We however curate the content and make sure that the pictures only show appropriate content and do e.g. not include persons, numberplates or other sensitive or inappropriate data.
Picture data is also categorized, providing you with meta information about those pictures so you can filter and arrange them as needed. Pictures are adapted to a target quality sufficient for viewing in a browser or app while optimizing bandwith usage. A thumbnail offers your users a preview of that picture while keeping bandwidth requirements minimal.
