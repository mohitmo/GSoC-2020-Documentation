# Speed Optimisations for cups-browsed: GSoC '20

Hello World!! I am Mohit Mohan, junior at Computer Science department at IIT Kanpur. I got selected in Google Summer of Code '20 to work with [Open Printing](https://openprinting.github.io/) under [The Linux Foundation](https://www.linuxfoundation.org/) on the project [**Speed Optimisations for cups-browsed**](https://summerofcode.withgoogle.com/projects/#4892000249184256).

### About the project

Cups-browsed, a daemon for browsing and filtering printers available on a network. But the time taken to create print queues for all the printers increases greatly as the number of printers increases. So from a users' perspective it is important to reduce the time taken to create the queues. Thus multi-threading is the way to do it, as we make some part of the code to run parallelly so that we can decrease the time it takes to create the queues for the printers.  

### Tasks Done

1. [Testing cups-browsed with different number of printers](https://github.com/mohitmo/Testing): Tested cups-browsed with different number of printers to find how much time it takes to [create print queues for all printers](https://github.com/mohitmo/Testing/blob/master/Test_result_without_cluster.txt) and in which [part of code](https://docs.google.com/spreadsheets/d/1Gldqr_x5y25Pd8DsT9eg4ba5BiArtWqbSbsx2QcQnFQ/edit#gid=0) it takes most of the time. I used [scripts](https://github.com/mohitmo/Testing/blob/master/script1.sh) running various instances of ippeveprinter to emulate printers on my systems.
2. [Design document for implementing multi-threading](https://github.com/mohitmo/design-document-cups-browsed): We figured out the approach to implement multi-threading in cups-browsed. To ease this and for future developers to reference, drafted a [design document](https://github.com/mohitmo/design-document-cups-browsed/blob/master/doc.md) for it.
3. [Parallelised handling of discovered printer instances](https://github.com/mohitmo/cups-filters/commit/db4eee4d4cf535aca9ff28b5d025d5ff519e0059): As we discover printer instances through Avahi, instead of passing resolve_callback() as callback, we pass resolver_wrapper() and it will create a new thread for calling resolve_callback(). With this approach we can process printer instances faster.
4. [Parallelised queue creation for the printers](https://github.com/mohitmo/cups-filters/commit/0d3965f8c6ddb5d914e86fa1b7a6250942c33d43): To create a queue, created function create_queue() that will be called in a new thread from update_cups_queues() suitably. 

### Commits

Commits can be found at this [link](https://github.com/mohitmo/cups-filters/commits?author=mohitmo).

### Tasks planned to be done

There are some things that we plan to do:

1. Optimising the current code, so that we can improve upon time taken to create queues even more.
2. Parallelise other events for cups-browsed, such as job processing and printer deletion.

### Acknowledgement 

I would like to thank my mentors [Till Kamppeter](https://github.com/tillkamppeter) and [Deepak Patankar](https://github.com/deepak0405) for guiding and helping me in this project. It was great experience working and communicating with them. I would also like to thank Aveek Basu for providing me this opportunity to have a very productive summer. 