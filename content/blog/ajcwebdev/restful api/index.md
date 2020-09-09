---
title: restful API
date: "2020-08-05"
description: representational state transfer application programming interface
---

*Summary of [restfulapi.net](https://restfulapi.net/)*

# What is REST

REST stands for REpresentational State Transfer. It is an architectural style for distributed hypermedia systems first presented in Roy Fielding's dissertation in 2000.

## Guiding Principles of REST

* **Client–server** – Separating user interface concerns from data storage concerns improves:
  * Portability of the user interface across multiple platforms
  * Scalability by simplifying the server components

* **Stateless** – Each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server.
  * Session state is therefore kept entirely on the client.

* **Cacheable** – Cache constraints require that the data within a response to a request be implicitly or explicitly labeled as cacheable or non-cacheable.
  * If a response is cacheable, then a client cache is given the right to reuse that response data for later, equivalent requests.

* **Uniform interface** – Applying the principle of generality to the component interface simplifies the overall system architecture and the visibility of interactions is improved. REST is defined by four constraints for obtaining a uniform interface:
  * identification of resources
  * manipulation of resources through representations
  * self-descriptive messages
  * hypermedia as the engine of application state

* **Layered system** – Hierarchical layers constrain component behavior.
  * Each component cannot “see” beyond the immediate layer with which they are interacting.

* **Code on demand (optional)** – Client functionality can be extended by downloading and executing code in the form of applets or scripts.
  * This simplifies clients by reducing the number of features required to be pre-implemented.

## Resource

Any information that can be named can be a resource:
* Document or image
* Temporal service
* Collection of other resources
* Non-virtual object (e.g. person)

### Resource Representation

REST uses a resource identifier to identify the particular resource involved in an interaction between components. The state of the resource at any particular timestamp is known as **resource representation**. A representation consists of:
* Data
* Metadata describing the data
* Hypermedia links which can help the clients in transition to the next desired state

### Media Type

The data format of a representation is known as a **media type**.
* Identifies a specification that defines how a representation is to be processed
* A RESTful API looks like hypertext
* Every addressable unit of information carries an address, either
  * Explicitly (link and id attributes)
  * Implicitly (derived from the media type definition and representation structure).

According to Roy Fielding:

>Hypertext (or hypermedia) means the simultaneous presentation of information and controls such that the information becomes the affordance through which the user (or automaton) obtains choices and selects actions. Remember that hypertext does not need to be HTML (or XML or JSON) on a browser. Machines can follow links when they understand the data format and relationship types.

### Self-Descriptive

Further, resource representations shall be **self-descriptive**: the client does not need to know if a resource is employee or device.
* It should act on the basis of media-type associated with the resource
* In practice you will end up creating lots of custom media-types (normally one media-type associated with one resource)

>Every media type defines a default processing model. For example, HTML defines a rendering process for hypertext and the browser behavior around each element. It has no relation to the resource methods GET/PUT/POST/DELETE/… other than the fact that some media type elements will define a process model that goes like “anchor elements with an href attribute create a hypertext link that, when selected, invokes a retrieval request (GET) on the URI corresponding to the CDATA-encoded href attribute.”

### Resource Methods

Another important thing associated with REST is **resource methods** to be used to perform the desired transition.
* A large number of people wrongly relate resource methods to HTTP GET/PUT/POST/DELETE methods.
* Fielding never mentioned any recommendation around method usage; he only emphasizes that it should be a uniform interface.
* Deciding that POST will be used for updating a resource instead of PUT is still considered RESTful.
* Ideally, everything that is needed to change the resource state shall be part of API response for that resource – including methods and in what state they will leave the representation.

>A REST API should be entered with no prior knowledge beyond the initial URI (bookmark) and set of standardized media types that are appropriate for the intended audience (i.e., expected to be understood by any client that might use the API). From that point on, all application state transitions must be driven by client selection of server-provided choices that are present in the received representations or implied by the user’s manipulation of those representations. The transitions may be determined (or limited by) the client’s knowledge of media types and resource communication mechanisms, both of which may be improved on-the-fly (e.g., code-on-demand).
>
>[Failure here implies that out-of-band information is driving interaction instead of hypertext.]

Query based API results should be represented by a list of links with summary information, not by arrays of original resource representations. The query is not a substitute for identification of resources.

## REST and HTTP are not the same

REST and HTTP are not same, but since REST also intends to make the web more streamline and standard, Fielding advocates using REST principles more strictly. And that’s from where people try to start comparing REST with web (HTTP). Fielding's dissertation does not mention any implementation directive or protocol preference.

In the REST architectural style, data and functionality are considered resources and are accessed using **Uniform Resource Identifiers (URIs)**.
* The resources are acted upon by using a set of simple, well-defined operations.
* The clients and servers exchange representations of resources by using a standardized interface and protocol – typically HTTP.

Resources are decoupled from their representation so that their content can be accessed in a variety of formats, such as:
* HTML
* XML
* plain text
* PDF
* JPEG
* JSON

Metadata about the resource is available and used to:
* control caching
* detect transmission errors
* negotiate the appropriate representation format
* perform authentication or access control

Every interaction with a resource is stateless. All these principles help RESTful applications to be simple, lightweight, and fast.