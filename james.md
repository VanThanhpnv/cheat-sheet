James stands for Java Apache Mail Enterprise Server.

This mail server is built with two goals in mind :

 - Being fully OpenSource (Apache 2.0 license)
 - Being easily customizable :
   - You can easily inplement / choose the backend you want. For each component of the mail server.
   - You can define via XML configuration how the mail will be processed.
   
This makes it easy to use James :
 - As a Mail Delivery Agent : A IMAP server on wich users have mailboxes
 - As a Mail Transfer Agent : A SMTP server that relays eMail
 
During these two weeks, we are going to work with two parts of this mail server :
 - With the mail processing unit. Mailet and Matchers are pieces of code that allows to customize the behaviour James should have when receiving emails.
 - With the mailbox. It is the unit in charge of persisting user e-mails.
 
Here is one architecture schema of James :

![](img/internal.png)

## Developping in James

First get the sources :
 - Fork https://github.com/PVN-Linagora/james-project
 - Then clone your new (forked) repository on your computer
 - Import it into Eclipse

You should have maven-3 installed as well as a Java 8 Java Runtime Environment.

We will not launch James during this set of practical works so no need to install docker.

## A little maven cheat sheet

To build the entire project issue :

```
mvn clean install --DskipTests
```

To run tests inside a project do (after building all) :

```
cd mailet/standard
mvn clean install
```

To run a specific class of test from maven : 

```
mvn -Dtest=NameOfTheClass -DfailIfNoTests=false -Pjpa -pl org.apache.james:artifact-id -am test

Example :

mvn -Dtest=JPAMailboxTest -DfailIfNoTests=false -Pjpa -pl org.apache.james:apache-james-mpt-imapmailbox-jpa -am test
```

You might also be able to run them in your IDE.

Note : JPA tests might need the command line.

