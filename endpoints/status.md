Mobility Tool+ Mobilities Status endpoint
=========================================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This endpoint allows the HEI to check the status of a previously sent mobility report.


Request method
--------------

 * Requests MUST be made with either HTTP GET or HTTP POST method. Servers MUST
   support both these methods. Servers SHOULD reject all other request methods.

 * Clients are advised to use POST when passing large number of parameters
   (servers MAY set a limit on their GET query string length).


Request parameters
------------------

Parameters MUST be provided in the regular `application/x-www-form-urlencoded`
format.


### `msg_id` (required)

Identifier of the report message we want to check the status of, as returned by
the report receiving party.


### `mobility_id` (optional, repeatable)

Identifiers of the mobilities we want to check the status of. It SHOULD be mobilities
that have been sent in the report of given `msg_id`, otherwise they will be ignored.
This parameter is used to limit the response. If not present, than the server MUST
return status of all the mobilities from the report.


Permissions
-----------

 * If the caller covers the HEI that sent the report with the given id,
   then he MUST be allowed to check its status.

 * All other callers SHOULD NOT be allowed access.


Handling of invalid parameters
------------------------------

 * General [error handling rules][error-handling] apply.

 * If the caller doesn't have permission to check status of the report with given id
   or the report does not exist, then server MUST respond with HTTP 404.
   
 * Mobility ids that where not present in the report of the given `msg_id`
   MUST be ignored.


Response
--------

Servers MUST respond with a valid XML document described by the
[status-response.xsd](status-response.xsd) schema. See the schema annotations for
further information.


[develhub]: http://developers.erasmuswithoutpaper.eu/
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
