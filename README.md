# This info is a bit of the crazy world of infosec which r00t-h4ck3r trys to fiddle with :)

# A puzzle of emails..(Phishing-pains)

It has been a intensive task for everyone in the infosec community. The techniques and tools used by adversories keep changing and the infosec community is still
lacking the right path for conducting training campaigns. 

There are many issues which arise while conducting a phishing training such as
   
         1)The infosec personnel of the company lack right amount of knowledge
         2)There is lack of resources
         3)Many more..

So i will explain many real world tactics as well as some old school stuff too . # Bonus(This post will help you to create your own approach for phishing which will help you in future)

Lets make this friendly for all level of people.

Phishing is nothing new and has been there since a long time and the volume of phishing attacks keep increasing day by day.
The approach which spammers as well as advanced threats such as nation state as APT's use keeps changing rapidly. But the security industry does not match te pace of these adversories as the are always outnumbered in may ways.

# Skip  (Only for n00b's)

To understand lets see what email is and how it works.

Electronic mail (email or e-mail) is a method of exchanging messages ("mail") between people using electronic devices. Invented by Ray Tomlinson
Some early email systems required the author and the recipient to both be online at the same time, in common with instant messaging. Today's email systems are based on a store-and-forward model. Email servers accept, forward, deliver, and store messages. Neither the users nor their computers are required to be online simultaneously; they need to connect only briefly, typically to a mail server or a webmail interface for as long as it takes to send or receive messages.

The basic Internet message format used for email is now defined by RFC 5322

Each email message has a header (the "header section" of the message, according to the specification), comprising a number of fields ("header fields"). Each field has a name ("field name" or "header field name"), which is followed by the separator character ":", and a value ("field body" or "header field body").

![alt text](https://proxy.duckduckgo.com/iu/?u=https%3A%2F%2Fupload.wikimedia.org%2Fwikipedia%2Fcommons%2Fthumb%2F7%2F72%2FEmail.svg%2F527px-Email.svg.png&f=1)

The diagram to the right shows a typical sequence of events that takes place when sender Alice transmits a message using a mail user agent (MUA) addressed to the email address of the recipient.[28]


The MUA formats the message in email format and uses the submission protocol, a profile of the Simple Mail Transfer Protocol (SMTP), to send the message content to the local mail submission agent (MSA), in this case smtp.a.org.

The MSA determines the destination address provided in the SMTP protocol (not from the message header), in this case b.org which is a fully qualified domain address (FQDA).
The part before the @ sign is the local part of the address, often the username of the recipient, and the part after the @ sign is a domain name.

The MSA resolves a domain name to determine the fully qualified domain name of the mail server in the Domain Name System (DNS).

The DNS server for the domain b.org (ns.b.org) responds with any MX records listing the mail exchange servers for that domain, in this case mx.b.org, a message transfer agent (MTA) server run by the recipient's ISP.[29]
smtp.a.org sends to mx.b.org using SMTP. 

This server may need to forward the message to other MTAs before it reaches the final message delivery agent (MDA).

The MDA delivers it to the mailbox of user bob.

Bob's MUA picks up the message using either the Post Office Protocol (POP3) or the Internet Message Access Protocol (IMAP).

 # Understanding a Email 
     
    An email consists of three vital components: 
                   the envelope, 
                   the header(s) 
                   the body of the message
    Understanding Email Header is a very important part for both the attacker's all well as for the infosec guys.
               
               1.An attacker can use it to do multiple attacks which we will discuss later on. 
               2.A infosec personnel can have a look at the header and analyze it for forensic purpose.
               
      You can have a look at these links which will explain you the email header in a very interactive way.
  
  # Understanding a Email Envelope
      
      Envelope is the communication between and SMTP Client and Server. See a sample envelope on the right side. Messages sent by client       are indicated by C: and server's responses are indicated by S: Following is true with an email envelope.
      
      The client and server first greet each other with a HELO command.

      Client sends a MAIL FROM command representing the sender's email address. This value is also used to send a non-delivery report         (NDR) when message cannot be delivered.
      
      The server response with a 250 OK if this sender is acceptable.
      
      Next, the client sends one or more recipient's email address using the RCPT TO command.
      Again, the server responds with a 250 OK, provided the recipient is acceptable. If the server returns a rejection code, the sender       will generate an NDR. In this case, the actual message will never get sent to the receiving SMTP server.
      
      # Important Points
      
      It is very easy to specify a fake/forged address in the MAIL FROM command
      The receiving server has the ability to check a few things, such as sender's IP address, MX record and FQDN before accepting any         email.
      
      Sample Envelope ( Here "C" stands for client and "S" stands for sender)
      
            S: 220 foo.com Service Ready
            C: HELO bar.com
            S: 250 OK
            C: MAIL FROM:<james.baker@xyzinc.com>
            S: 250 OK
            C: RCPT TO:<mary.jane@abcinc.com>
            S: 250 OK
            C: DATA
            S: 354 Start mail input;
            C: Actual email is sent here
            C: .
            S: 250 OK
            C: QUIT
            
 # Understanding a Email Header
 
        1) Each email has a header assoicated with it and mxtoolbox explains how to view it the best way
        
            https://mxtoolbox.com/Public/Content/EmailHeaders/
        
        2) How to view e-mail headers explained by Microsoft
            
            ./https://support.office.com/en-us/article/View-internet-message-headers-cd039382-dc6e-4264-ac74-c048563d212c
           
        3) How to view e-mail headers explained by Google
            
            https://support.google.com/mail/answer/29436?hl=en 
           
          
 
# When are these values used

      Envelope From (RFC5321.MAIL FROM)
         Used by the SMTP server to generate NDR
         Used by SPF filter to determine if it came from the designated IP address.

      Header From (RFC5322.FROM)
         Used by the email client to display information in the From field.
         Used by DMARC filter to confirm if the message is authentic
   
   
