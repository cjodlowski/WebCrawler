### High level approach
    Our code began with the starter code which implemented connection to the server using HTTP/1.0
    We started off by changing the message sent to use HTTP/1.1 to connect to the server.  In the login
    method after we send the first get message we then send a post message containing the username and
    passwork from the command line to log into the webpage.  From the responce we get the csrftoken
    and the sessionid which we later use in the rest of our messages. After we log into the webpage
    we then search the page for links using MyHTMLParser which we then add to the queue list.  We also
    handle the data using MyHTMLParser to look for any flags in this page.  We then go through each
    page in the queue repeating the process.  When we get the page we also look at the connection status
    and the response code.  If the connection status is closed we reconnect to the socket and send a get
    message.  If we get a response code that is not 200 we deal with the error and do not parse through
    the data.  To avoid looping we have a list of all visited pages and check the new page we are going to
    against the list before we go to it.  If it is in the list we skip over that page.
    
    
### Challenges 
    Some challenges that we faces were that our code was taking a long time and may have been looping. We
    had thought that were checking the visited list before we added to the queue but it seemed like we
    were missing something. To fix this we added another check in the main run loop to check the page against
    the visited list before going to said page.  Another challenge that we faced was that the connection would
    randomly close out on use.  In response added another check when we recieved a response to check the 
    connection status and we would reconnect if the status was closed.
    
### Testing
    For testing we first tried to connect to the server using HTTP/1.1.  After we were able to connect we 
    sent a post message to log in to the server.  At first it wasn't working so we used piazza to help test
    and found out that we needed the csrfmiddlewaretoken to connect.  After this we tested to see if we could 
    get all of the flags.  We saw that it was taking a very long time and was not getting all the flags so 
    we concluded that we were looping somewhere so we fixed it.
    
### Features 
    Some features that we implemented that I think were good is the MyHTMLParser which allows us to more 
    easily parse through the HTML response. We use it to check for links in the page and to check for flags
    that may be found in said page. This is more effective than using the find method that we had used earlier.
    
