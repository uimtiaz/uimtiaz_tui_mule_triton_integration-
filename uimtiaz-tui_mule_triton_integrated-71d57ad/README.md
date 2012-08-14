Project name: tui_mule_triton_integrated

XML code of all POCs is merged into a single mule config file.
It is also possible to separate all the code in different mule config files for easier readability.


The former tui_mule_auth is the HTTP entry point.
The former tui_mule_triton now has an inbound VM endpoint.
In the triton_main_vm_flow, the integration of tui_cache_ornot_poc takes place after the choice component. When the class==CACHE the test-cache-availability flow is called and if the ‘availability’ cache is not available then the call is routed to the SEARCH class. The code of tui_cacheornot_poc has been simplified to only return true/false.

About mongodb: the data for ‘availability’ and ‘authentication’ collections persists when the mongodb process stops or crashes. All it takes is to restart the process.
These 2 collections should only get repopulated based on a business need.

Think of adding ‘channel’ field to the webwumst data dump. The benefit is to avoid passing the channel url param for each call.

In flow, tui_mule_auth, edit the 2 VM outbound endpoints: triton.stub.Q.1 & triton.stub.Q.2 queue names and replace them by: tritonQ

Delete the 2 mule-triton-stub flows. They were only meant to test in isolation. (outside the VPN).


