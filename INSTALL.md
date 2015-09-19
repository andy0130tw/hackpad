# INSTALLATION INSTRUCTIONS
INSTALLING ON UBUNTU, FOR EXAMPLE

## Installing the dependencies from `apt-get`:
  * Sun Java JDK 7: `default-jdk`
  * Scala 2.11: `scala`
    * sudo apt-get remove scala-library scala
    * sudo wget www.scala-lang.org/files/archive/scala-2.11.7.deb
    * sudo dpkg -i scala-2.11.7.deb
    * sudo apt-get update
    * sudo apt-get install scala
  * MySQL: `mysql-server` and `mysql-client`

## Configuring
* Edit the file bin/exports.sh (and optionally `etherpad/bin/etherpad.default`) and change the paths to
  match your system.

  For my machine, 
    ```
      export SCALA_HOME="/usr/share/scala"
      export SCALA="$SCALA_HOME/bin"
      export SCALA_LIBRARY_JAR="$SCALA_HOME/lib/scala-library.jar"
    ```

* Run `bin/build.sh`

* Run `contrib/scripts/setup-mysql-db.sh`

* Copy `etherpad/etc/etherpad.localdev-default.properties` to `etherpad/etc/etherpad.local.properties`
* Edit `etherpad/etc/etherpad.local.properties` and set
  * etherpad.superUserEmailAddresses
       Example: etherpad.superUserEmailAddresses = name1@example.com,name2@example.com
  * topdomains
       Example: topdomains = yourhostname.com,localhost

* You can now run etherpad via `bin/run.sh`.  Wait for the HTTP server to start
  listening, then visit `http://localhost:9000`.

* Create an account in development
  * Go through the sign up flow.  At this point, you will have created an
    account, but it needs to be validated.  If this were production, you would
    go to your email to click a link in a verification email, but since your
    development environment does not send email, we will resort to haxx.
  * Inspect the `email_signup` table in MySQL and find the row with your email
    address.  Note the token.
  * Visit `http://localhost:9000/ep/account/validate-email?email=YOUR_EMAIL&token=TOKEN`
  * Hurrah, you now have an account!

* If you want emoji support go to https://github.com/github/gemoji/tree/master/images/emoji/unicode
  and copy the images into etherpad/src/static/img/emoji/unicode/

