

# Sanad - An Interactive Robot Companion for MCI Patients
Sanad - an Arabic word meaning "support" or "something to lean on", it is a robot that was developed in order to support, and give a hand to MCI (Mild Cognitive Impairment) patients. 
Sanad can assist three different kind of users: patients, caregivers and family members by speech commands or using a touch screen. Its main functionality will be the ability to identify registered faces 
so it can remind the patient about their relationship to them and who they are. It can also help in urgent situations by either calling family members or by taking advice from its own learned chatbot. 
You can also modify Sanad voice to imitate other people's voice for the patient to understand and recognize the voice they are familiar with. 
It can also remind patients about Activities of Daily Living (ADL) and Instrumental Activities of Daily Living (IADLs). 
Sanad will be a great companion for elderly people and support them with their daily living activities.

## Getting Started
 
#### Check Compatibility:
Make sure your computer runs one of the supported Operating System:

|    **OS**       | **Version**                               |
|:--------------|:---------------------------------------|
| *Linux*       | Ubuntu 16.04 Xenial Xerus - 64-bit only |
| *Windows*     | Microsoft Windows 10 - 64-bit only      |
| *Mac*         | Mac OS X 10.12 Sierra                   |

#### Hardware Prerequisites:
> Pepper *(Version 1.8A)*

#### Software Prerequisites:
>1. Android Studio *(Version 2.3 or higher)*
>2. Java Development Kit (JDK) *(Version 1.8 or higher)*
>3. Pepper SDK Plug-in (QiSDK)

#### SDK Subscription  Prerequisites:
> Luxand FaceSDK


## Software Installation Guide:
* #### Java Development Kit (JDK):
> [Download](https://www.oracle.com/java/technologies/javase-downloads.html) **Java SE**

* #### Android Studio:
> [Download](https://developer.android.com/studio) **Android Studio**
>
>In Android Studio download the following:-
>1. Install **Android SDK** *(Version **Android 9.0(pie)**)*
>2. Install **Build-Tools** *(Version **Build-Tools 28.0.3**)*
>3. Install **Pepper SDK Plugin**
>##### For *Windows OS* check "Additional steps for Windows" in the [QiSDK Documentation](https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/ch1_gettingstarted/installation.html)
>###### For more guidance/steps to configure QiSDK in Android Studio follow this [QiSDK Documentation](https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/ch1_gettingstarted/installation.html)


* #### Pepper Plug-in:
>Once **Pepper SDK Plugin** is installed, your last step for setting up the environment is to download the tools for developing robot application.
>1. Choose **Tools** > **Pepper SDK** > **Robot SDK Manager** or you can also click the **Robot SDK Manager**  ![image7](https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/_images/robot_sdk_manager_btn.png) tool
>2. Choose **API 4**
>3. Click apply


## SDK Subscription Guide:
* #### Luxand FaceSDK:
>1. Open [Luxand FaceSDK subscription](https://www.luxand.com/facesdk/trial/)  webpage and subscribe for the free 14 days trial.
>2. You will then receive a subscription code to your email store it as we are going to use it in the next section.


## Sanad Installation Guide
### 1. Install Sanad:
1. Click download from GitLab
2. Open Android Studio
3. Click on *"Open an existing Android Studio Project"* button
4. Navigate to the folder downloaded and select the file called **"ProjectInterface"**
5. Wait for android studio to build the project and continue to the next section!

### 2. Check Android Studio project configuration ( build.gradle ):
Open *"Gradle Scripts"* then *"build.gradle"* for *"app"* and check the following:
> ```
> compileSdkVersion  28  
> buildToolsVersion "28.0.3"
> and
> minSdkVersion 23  
> targetSdkVersion 28
> ```

### 3. Connecting to Pepper
##### To run an application on a real robot, there are 2 steps:
##### 1.  Preparing a robot for connection:
In Pepper tablet go to *"Home"* > *"Settings"* 

Make sure:
- the **Developer mode** is activated.
- the **Developer options** / **Debugging** / **ADB** is also activated

##### 2. Connecting to a real robot:
1. *"Tools"*  >  *"Pepper SDK"*  >  *"Connect"*  or Click the  ![connect_btn](https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/_images/connect_btn.png)  *Connect*  button.
2. Select one of the robots in the list.
3. Enter the password and click *"OK"* button.
4. Enter the IP address of the robot tablet.
5. Wait for the complete connection.
6. Once connected to a real robot, you should see this alert
>![../_images/connection_succeed.png](https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/_images/connection_succeed.png)

####  4. Update Subscription Key:
1. Copy the subscription key from the Luxand FaceSDK email.
2. Navigate to *"Main Activity"*.
3. Go to *"onCreate"* method and replace the key in red with key received.

> ```java
> int res = FSDK.ActivateLibrary("NQUZSSKAvEoCBkoN1a6Ha6jdbTdWT6deMfhb2n9N7I8nrN/oqe061n0LJ" +  
>      "U03LAjih89b2dDeKp9Ukt/NWZ28f/7N1g4P4i3G+jYX5HluMhpDOb1fmExxRojKXsg9hN0bDFNq1zg/rDXq06RKB2FFf3CcEfL5sfVd55oTWLk8nB4=");
> ```

#### 5. Run!
Make sure that:
- the selected run configuration of your project is  `app`, otherwise, select it.
- the selected device is  `ARTNCORE  LPT_200AR`, otherwise, select it.

>![../_images/run_configuration_toolbar_real_robot.png](https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/_images/run_configuration_toolbar_real_robot.png)

Then click the  ![run_btn](https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/_images/run_btn.png)  **Run**  button.


## Sanad Functionalities:
### Controlling Sanad:
**1. Speech Commands**
Sanad can execute an action by listening to user requests using 'Listen' object and match it with the predefined commands to perform the required task. 

*Attached below is the syntax on how to predefine and action and how to execute it, moreover also shown is the code used:-*

The syntax for using 'Listen':
> ```java
> // Here you create a phrase set. Phrase set can contain one or 
> // several phrases that we want Sanad to recognise. 
> // You can replace "Hello" with your custom phrase or phrases.
> PhraseSet phraseSet = PhraseSetBuilder.with(qiContext)
>                                      .withTexts("Hello")
>                                    .build();
>                                    
>// Here you build the action using the phraseSet defined above.
>Listen listen = ListenBuilder.with(qiContext)
>                             .withPhraseSet(phraseSet)
>                             .build();
>                             
>// Then run the action synchronously or asynchronously depending
>// on the thread you are working on. 
>// For more information visit https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/ch2_principles/sync_async.html
>ListenResult listenResult = listen.run();
>```

The syntax to execute an action based on the predefined phrase:
> ```java
>// Identify the matched phrase set
>PhraseSet matchedPhraseSet = listenResult.getMatchedPhraseSet();
>
>// Check if the matchedPhraseSet equals the phraseSet defined and 
>// based on it execute an action
>if (PhraseSetUtil.equals(matchedPhraseSet, phraseSet)) {
>// Insert actions you want Sanad to execute if he heard the 
>// correct phrase**
>}
>else{
>// Insert action you want Sanad to execute if he did not hear
>// the correct phrase
>}
> ```

Sanad code snippet:
> ```java
> // Create the phrase set
> PhraseSet phraseSetCall = PhraseSetBuilder.with(qiContext) 
> // Add the phrases you want Sanad to recognise
> .withTexts("Call family", "Help", "Call", "Call Emergency") 
>  // Build the action 
>  .build();
>
> // Create the phrase set
> PhraseSet phraseSetRecognize = PhraseSetBuilder.with(qiContext) 
> // Add the phrases you want Sanad to recognise
> .withTexts("Recognize", "Recognize face", "who is this", "recognize who came in", "who came in") 
> // Build the action 
> .build();
>
>// Create the phrase set
>PhraseSet phraseSetChatbot = PhraseSetBuilder.with(qiContext) 
>		// Add the phrases you want Sanad to recognise
> 		.withTexts("Open chatbot", "Open Sanad bot", "chat") 
> 		// Build the action 
> 		.build();
>
>Listen listen = ListenBuilder.with(qiContext) // Create the builder with the QiContext.  
>		// Set the PhraseSets to listen to.  
>		.withPhraseSets(phraseSetCall, phraseSetRecognize, phraseSetChatbot)
>		// Build the listen action.
>		.build();
>
>ListenResult listenResult = listen.run();  
>
>// Identify the matched phrase set.  
>PhraseSet matchedPhraseSet = listenResult.getMatchedPhraseSet();  
>
>// Check if matchedPhraseSet equals the call phraseSet then execute the call action
>if (PhraseSetUtil.equals(matchedPhraseSet, phraseSetCall)) 
>{
>if (clientThread != null) 
>   {  
>    clientThread.sendMessage(familyMember.getNumber());
>   }
>}
>else if (PhraseSetUtil.equals(matchedPhraseSet, phraseSetRecognize))
>{
>   findHumansAround();
>}
>else if (PhraseSetUtil.equals(matchedPhraseSet, phraseSetChatbot))
>{
>   startActivity(new Intent(PatientMenu.this, SanadChatBot.class));
>}
>else {  
>   say(qiContext, "Say your speech command again");  
>}
> ```
___
**2. Assistive Touch**
Sanad can execute an action by pressing a button to perform the required task. 

*Attached below is the syntax on how to predefine and action and how to execute it, moreover also shown is the code used:-*

The syntax to execute an action using Button:
> ```java
> // Define a Button
> Button buttonName = findViewById(R.id.buttonID)
>
> // Set on click listener to the button
> buttonName.setOnClickListener(this);
>
>// Use switch case inside the onClick() method to check which button is pressed and execute 
>// its action
>@Override  
>public void onClick(View v) {
>switch (v.getId()) 
>{
>	case R.id.buttonID:
>			//Action want to be executed
>			break;
>}
>}
> ```

Sanad code snippet:
> ```java
>@Override  
>public void onClick(View v) {  
>  switch (v.getId()) {  
>        case R.id.callEmergencyPButton:  
>                if (clientThread != null) {  
>                      if (familyMember != null) {  
>                        showMessageToClient("Connected");
>                        clientThread.sendMessage(familyMember.getNumber());
>                        istenBuilder();  
>                        } else {  
>                        Toast.makeText(PatientMenu.this, "Could not find emergency number", Toast.LENGTH_SHORT).show();  
>                        }  
>                   } else {  
>                   showMessageToClient("Unable to send message to server");  
>                   }  
>                   break;
>       case R.id.setAlarmPButton:  
>         	setReminder(); 
>			break; 
>		case R.id.cancelAlarmPButton:  
>			cancelReminder();  
> 			break;
>	}
>}
	
	
### Sanad Main Features:
**1. Sanad's Project Database**
For this project a cultivated database was developed called “SanadProject.db” that holds six varied tables to store different data for each patient, family member, caregiver, patient medicine, patient appointment and their reminders. All of the mentioned tables have a unique primary and foreign key which have the function of linking tables to establish a specialised relationship as shown in the code below:-

1. Create a new class that extends SQLiteOpenHelper
2. Create String variables for Database, table names and their headers:-**
> ```java
> // Database name
>private static final String DATABASE_NAME = "SanadProject.db";
>
>// Caregiver table names and headers
>public static final String COLUMN_CAREGIVER_ID = "caregiver_id";  
>public static final String COLUMN_CAREGIVER_NUMBER = "caregiver_number";  
>public static final String COLUMN_CAREGIVER_HOSPITAL = "caregiver_hospital";  
>public static final String COLUMN_CAREGIVER_ROLE = "caregiver_role";  
>public static final String COLUMN_CAREGIVER_IMAGE_PATH = "face_image_path";  
>public static final String COLUMN_CAREGIVER_FACE_TEMPLATE = "face_template";
>
>// Patient table and its headers
>public static final String PATIENT_TABLE = "patient_table";  
>public static final String COLUMN_PATIENT_ID = "patient_id";  
>public static final String COLUMN_PATIENT_NAME = "patient_name";  
>public static final String COLUMN_PATIENT_NUMBER = "patient_number";  
>public static final String COLUMN_PATIENT_IMAGE_PATH = "face_image_path";  
>public static final String COLUMN_PATIENT_FACE_TEMPLATE = "face_template";  
>// The below column header will be assigned as a foreign key to the caregivers tables
>public static final String COLUMN_PATIENT_CAREGIVER_ID = "caregiver_id";
>```

3. Create an SQL Statement:-
>```java
>// caregiver create table sql statement  
> private static final String SQL_CAREGIVER_CREATE_TABLE = "CREATE TABLE "
>  + COLUMN_CAREGIVER_ID + " INTEGER PRIMARY KEY AUTOINCREMENT, "  
>  + COLUMN_CAREGIVER_NAME + " TEXT NOT NULL, "  
>  + COLUMN_CAREGIVER_NUMBER + " TEXT NOT NULL, "  
>  + COLUMN_CAREGIVER_ROLE + " TEXT NOT NULL, "  
>  + COLUMN_CAREGIVER_HOSPITAL + " TEXT NOT NULL, "  
>  + COLUMN_CAREGIVER_IMAGE_PATH + " VARCHAR(50) NOT NULL, "  
>  + COLUMN_CAREGIVER_FACE_TEMPLATE + " BLOB NOT NULL "  
>  + ")";
>   
>   // patient create table sql statement  
>private static final String SQL_PATIENT_CREATE_TABLE = "CREATE TABLE "
>  + PATIENT_TABLE + "("  
>  + COLUMN_PATIENT_ID + " INTEGER PRIMARY KEY AUTOINCREMENT, "  
>  + COLUMN_PATIENT_NAME + " TEXT NOT NULL, "  
>  + COLUMN_PATIENT_NUMBER + " TEXT NOT NULL, "  
>  + COLUMN_PATIENT_IMAGE_PATH + " VARCHAR(50) NOT NULL, "  
>  + COLUMN_PATIENT_FACE_TEMPLATE + " BLOB NOT NULL, "  
>  + COLUMN_PATIENT_CAREGIVER_ID + " INTEGER NOT NULL "  
>  + ")";
>```
4. Create Database in DatabaseHelper method :-
> ```java
>public DatabaseHelper(Context context) {  
>    // Give the database name and the version in the super statement to create the db
>    super(context, DATABASE_NAME, null, DATABASE_VERSION);  
>}
>```
5.Create onCreate method to execute tables:-

> ```java
>@Override  
>public void onCreate(SQLiteDatabase db) {  
>    db.execSQL(SQL_CAREGIVER_CREATE_TABLE);  
>    db.execSQL(SQL_FAMILY_CREATE_TABLE);  
>    db.execSQL(SQL_PATIENT_CREATE_TABLE);  
>    db.execSQL(SQL_APPOINTMENT_CREATE_TABLE);  
>    db.execSQL(SQL_MEDICINE_CREATE_TABLE);  
>    db.execSQL(SQL_REMINDERS_CREATE_TABLE);  
>} 
>```
6. Finally the onUpgrade method:-

> ```java
> // Will check if tables already exist or not
>@Override  
>public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {  
>    Log.w(TAG, "Upgrading the database from version " + oldVersion + " to " + newVersion);  
>  
>  db.execSQL("DROP TABLE IF EXISTS " + CAREGIVER_TABLE);  
>  db.execSQL("DROP TABLE IF EXISTS " + FAMILY_TABLE);  
>  db.execSQL("DROP TABLE IF EXISTS " + PATIENT_TABLE);  
>  db.execSQL("DROP TABLE IF EXISTS " + APPOINTMENTS_TABLE);  
>  db.execSQL("DROP TABLE IF EXISTS " + MEDICINE_TABLE);  
>  db.execSQL("DROP TABLE IF EXISTS " + REMINDER_TABLE);  
>  
>  onCreate(db);  
>}
>```
___
**2. Emergency Calls**
Emergency call functionality is executed whenever the user clicks on the "Call Emergency" button or says "Call Emergency" and other predefined commands. The functionality will send a push notification from pepper's tablet to the phone connected on the same wifi to make the call. Since the tablet does not have sim-card.

**Call emergency action code is shown below:-**

Client side of the functionality:-

> ```java
>// Button to execute action
>// TextView to show the output of the connection between client and server
>// Handler to send and process Message and Runnable objects associated with a thread's
>// ClientThread class that initialise a connection with the server to send and receive messages.
>private Button callEmergencyBtn;  
>private TextView callMessageEdit;  
>private Handler handler;  
>private ClientThread clientThread;
>
>// Intialise the handler in onCreate() Method and show a message
>handler = new Handler();  
>showMessageToClient("Connecting to Server...");
>
>// When the button is pressed
>case R.id.callEmergencyPButton:  
>    // Check if clientThread is not null and it is connected to server
>    if (clientThread != null) {  
>        if (familyMember != null) { 
>            // If clientThread is connected it will show this message to client
>            showMessageToClient("Connected");  
>            // Then send a message to the server with the family member number stored in the above database to make the call
>            clientThread.sendMessage(familyMember.getNumber());  
>            
>          } else {  
>               Toast.makeText(PatientMenu.this, "Could not find emergency number", Toast.LENGTH_SHORT).show();  
>          }  
>     } else {  
>         // If the client is not connected to the server it will show this message to the client
>         showMessageToClient("Unable to send message to server");  
>  }  
>    break;
>
>// showMessageToClient method is used to handle the messages received from server
>public void showMessageToClient(final String message) {  
>    handler.post(new Runnable() {  
>        @Override  
>         public void run() {  
>             // It sets the TextEdit with the message entered
>             callMessageEdit.setText(message); }  
>        });  
>}
>
>// The below code is in onDestroy to stop the connection with the server.
>if (clientThread != null) {  
>    clientThread.sendMessage("Disconnect");  
>    // initialise clientThread to null
>    clientThread = null;  
>}
>```
>

ClientThread Class:
> ```java
>// ClientThread implements Runnable which is an interface used for creating a new thread class
>class ClientThread implements Runnable {  
>  
>  // PatientMenu to show messages to the client
>  // Port number used to connect to server
>  // and finally the ip address of the server
>     private PatientMenu patientMenu;  
>     private static final int SERVERPORT = 8080;  
>     private static final String SERVER_IP = "155.245.23.244";  
>  
>  // Socket is an endpoint for communication between two machines
>  //BufferedReader reads texts from input stream
>     private Socket socket;  
>     private BufferedReader input;  
>  
>     @Override  
>      public void run() {  
>        try {  
>            // Determines the ip address of the host
>            InetAddress serverAddress = InetAddress.getByName(SERVER_IP);
>            // Initialise the socket with port number and serverAddress determined above  
>            socket = new Socket(serverAddress, SERVERPORT);  
>  
>            while (!Thread.currentThread().isInterrupted()) {  
>  
>                // Get mesage from server
>                this.input = new BufferedReader(new InputStreamReader(socket.getInputStream()));  
>                String message = input.readLine();  
>                // If client did not connect with the server
>                if (null == message || "Disconnect".contentEquals(message)) {  
>                    // Tests whether the current thread has been interrupted
>                    Thread.interrupted();  
>                    message = "Server Disconnected.";  
>                    //Show message to client that server disconnected
>                    patientMenu.showMessageToClient(message);  
>                    break;  
>                }  
>                patientMenu.showMessageToClient("Server: " + message);  
>            }  
>        } catch (UnknownHostException e1) {  
>            e1.printStackTrace();  
>        } catch (IOException e1) {  
>            e1.printStackTrace();  
>    }  
>  }  
>  
>    // sendMessage method is used to send data to server
>    public void sendMessage(String clientMessage) {  
>        new Thread(new Runnable() {  
>            @Override  
>             public void run() {  
>                try {  
>                    //if socket is not null 
>                    if (null != socket) {  
>                        // printWriter prints an Object and then terminates the line
>                        PrintWriter out = new PrintWriter(new BufferedWriter(  
>                                new OutputStreamWriter(socket.getOutputStream())),  true);  
>                        // Prints the client message on screen        
>                        out.println(clientMessage);  
>                     }  
>                } catch (Exception e) {  
>                    e.printStackTrace();  
>                }  
>            }  
>        }).start();  
>     }  
>}
>```

Server side of the functionality:-
> 
> ```java
> //First add this in manifest file:
> "<uses-permission android:name="android.permission.CALL_PHONE/>"
> 
> // Handler to handle messages sent and received
> // ServerSocket create a server with the specified port and local IP address to bind to
> // Socket is an endpoint for communication between two machine
> private Handler handler;
> private ServerSocket serverSocket;  
> private Socket tempClientSocket;  
> Thread serverThread = null;  
>  
>public static final int SERVER_PORT = 8080;
>
>//Initialise handler and server thread and start the server in onCreate()
>handler = new Handler();
>this.serverThread = new Thread(new ServerThread());  
>this.serverThread.start();
>
>// sendMessage method is used to send data to client
>private void sendMessage(final String message) {  
>    try {  
>        // we first check if clientsocket is not null
>        if (null != tempClientSocket) {  
>            //create new thread to handle messsages
>            new Thread(new Runnable() {  
>                @Override  
>                public void run() {  
>                     // printWriter prints an Object and then terminates the line
>                    PrintWriter out = null;  
>                    try {  
>                        // try to send message to client
>                        out = new PrintWriter(new BufferedWriter(  
>                                new OutputStreamWriter(tempClientSocket.getOutputStream())), true);  
>                    } catch (IOException e) {  
>                        e.printStackTrace();  
>                    }  
>                    out.println(message);  
>                  }  
>            }).start();  
>         }  
>    } catch (Exception e) {  
>        e.printStackTrace();  
>    }  
>}
>
>class ServerThread implements Runnable {  
> 
>    @Override  
>  public void run() {  
>        // Create a Socket variable
>        Socket socket;  
>        try {  
>            // Initialise a serverSocket with the server port
>            serverSocket = new ServerSocket(SERVER_PORT);  
>        }catch (IOException e){  
>            e.printStackTrace();  
>            // show error message on server 
>            showMessage("Error Starting Server : " + e.getMessage());  
>        }  
>        // if serverSocket is not null and is not interrupted
>        if (serverSocket != null){  
>            while (!Thread.currentThread().isInterrupted()){  
>                try{  
>                    // if current thread is not interrupted, accept the socket  and create connectinThread and start it
>                    socket = serverSocket.accept();  
>                    CommunicationThread commThread= new CommunicationThread(socket);  
>                    new Thread(commThread).start();  
>                 }catch (IOException e){  
>                    e.printStackTrace();  
>                    showMessage("Error communicating to client: " + e.getMessage());  
>                }  
>            }  
>        }    
>    }  
>}
>
>class CommunicationThread implements Runnable {  
>  
>    // Socket is an endpoint for communication between two machine
>    // BufferedReader reads texts from input stream
>    private Socket clientSocket;  
>    private BufferedReader input;  
>  
>    // Method to initialise the clientsocket and start communication
>    public CommunicationThread(Socket clientSocket) {  
>        this.clientSocket = clientSocket;  
>        tempClientSocket = clientSocket;  
>        try {  
>            // get the input from client
>            this.input = new BufferedReader(new InputStreamReader(this.clientSocket.getInputStream()));  
>         } catch (IOException e) {  
>              e.printStackTrace();  
>              showMessage("Error Connecting to Client!!");  
>         }  
>         showMessage("Connected to Client!!");  
>         }  
>  
>    public void run() {  
>         while (!Thread.currentThread().isInterrupted()) {  
>            try {  
>                // read line from input
>                String read = input.readLine();  
>                // if input equals to disconnect and null
>                if (null == read || "Disconnect".contentEquals(read)) {  
>                    Thread.interrupted();  
>                    read = "Client Disconnected";  
>                    showMessage("Client : " + read);  
>                    break;  
>                }  
>                // will sow message received and check if the message is a 
>                // number then send it to onEmergency Call
>                showMessage("Client : " + read);  
>                if (read.matches("^[0-9]*$")){  
>                    onEmergencyCall(read);  
>                    sendMessage("calling a number ");  
>  
>                 }  
>            } catch (IOException e) {  
>                e.printStackTrace();  
>            }  
>  
>        }  
>    }  
>  
>     // Method to make a phone call 
>    public void onEmergencyCall(String userInput){  
>        // We first check for permission to make phonecall
>        // if we dont have the permission ask for it
>        if (ContextCompat.checkSelfPermission(ServerActivity.this,  
>                          Manifest.permission.CALL_PHONE) != PackageManager.PERMISSION_GRANTED) {  
>                          
>                 ActivityCompat.requestPermissions(ServerActivity.this,  
>                      new String[]{Manifest.permission.CALL_PHONE}, 1);  
>                      
>         } else {  
>            // if we have permission we will use intent to make a phonecall
>            Intent intent = new Intent(Intent.ACTION_CALL);  
>            intent.setData(Uri.parse("tel:"+userInput));  
>            startActivity(intent);  
>            }  
>      }  
>}
>
>// The below code is in onDestroy to stop the connection with the server.
>if (clientThread != null) {  
>    clientThread.sendMessage("Disconnect");  
>    // initialise clientThread to null
>    clientThread = null;  
>}
> ```
___
**3. Face Recognition**

**There are two thorough processes of face recognition;**
1.  It begins with a detailed process of face detection which consists of; extracting and fixating the image and following it with the function of normalisation of the landmarks of the face such as; the eyes, mouth and the nose. Then extracting and selecting the facial features.

> ```java
> //This variable uses the service 'HumanAwareness' found in QiSDK which expose actions and properties related to humans
> private HumanAwareness humanAwareness;
>
>//We have to initialise humandAwareness in onRobotFocusGained() as follows:
>humanAwareness = qiContext.getHumanAwareness();
>
>//The below method will find humans around and send it to another method called retrieve faces to get the detected face
>private void findFacesAround() {  
>
>          //Checks if there is any human around  
>          if (humanAwareness != null) {  
>               Future<List<Human>> humansAroundFuture = >humanAwareness.async().getHumansAround();  
>
>               humansAroundFuture.andThenConsume(humansAround -> {  
>                  //If humans detected it will send the object to detect the face otherwise pepper will say the following statement.
>                  if (humansAround.size() != 0) {  
>                        retrieveFaces(humansAround);  
>                  } else {  
>                        Log.e(TAG, "Face not detected. Press capture again");  
>                        sayAsync(qiContext, "Face not detected. Press capture again");  
>                     }  
>             });  
>        }  
>}
>```
> After finding the people around we will send the humansAround to retrieveFaces method below which will loop around the humans and extract the faces detected to store it for face recognition:
> 
> ```java 
>private void retrieveFaces(List<Human> humans) {  
>  
>  //A for loop to go through humans detected and extract their faces  
>  for (int i = 0; i < humans.size(); i++) {  
>        Human human = humans.get(i);  
> 
>        // Get the human position and put it in a frame.
>        Frame humanFrame = human.getHeadFrame();  
>        
>        // Get the face image and put in a byteBuffer 
>        ByteBuffer facePictureBuffer = human.getFacePicture().getImage().getData();  
>        facePictureBuffer.rewind();  
>        int pictureBufferSize = facePictureBuffer.remaining();  
>        byte[] facePictureArray = new byte[pictureBufferSize];  
>        facePictureBuffer.get(facePictureArray);  
>  
>        // Check if the robot has an empty picture (this can happen when he detects a human but not the face).  
>        if (pictureBufferSize != 0) {  
>         
>            // Put the face image in a bitmap to save it in the database
>            Bitmap facePicture = BitmapFactory.decodeByteArray(facePictureArray, 0, pictureBufferSize);  
>  
>            //It will save the image in database and on device and after saving 
>            //it it will store its path in mCurrentPhotoPath to send it to execute method in DetectFaceInBackground()
>            saveImage(facePicture);  
>  
>            if (mCurrentPhotoPath != null) {  
>                 //If photo is saved it will execute the picture to DetectFaveInBackground to extract the facial features template from the 
>                 //face and store it for later use with recognition
>                 new DetectFaceInBackground().execute(mCurrentPhotoPath);  
>             }  
>        } else {  
>               // If face not detected it will say the phrase below 
>               sayAsync(qiContext, "Face not detected. Press capture again");  
>           }  
>       }  
>}
>```
>The class below will receive the photo path and extract the facial features from it and draw a rectangle around the face using Luxand FaceSDK

> ```java
>private class DetectFaceInBackground extends AsyncTask<String, Void, String> {  
>    protected FSDK.TFacePosition faceCoords;  
>    protected String picturePath;  
>    protected FSDK.HImage picture;  
>    protected int result;  
>    protected boolean facesMatch;  
>    protected FSDK.FSDK_FaceTemplate faceTemplate;  
>  
>    @Override  
>    protected String doInBackground(String... params) {  
>        String log = new String();  
>        picturePath = params[0];  
>        faceCoords = new FSDK.TFacePosition();  
>        faceCoords.w = 0;  
>        picture = new FSDK.HImage();  
>        // Load the image from the file to an HImage
>        result = FSDK.LoadImageFromFile(picture, picturePath);  
>        // Check if it was loaded successfully 
>        if (result == FSDK.FSDKE_OK) {  
>               // if it was loaded successfully we will use FSDK.DetectFace to detect the face with the faceCoords initialised above
>               result = FSDK.DetectFace(picture, faceCoords);  
>               
>               // Check if it was detected successfully 
>               if (result == FSDK.FSDKE_OK) {  
>                   // if face was detected we will extract a template for the face and store it in faceTemplate object for later use
>                   faceTemplate = new FSDK.FSDK_FaceTemplate();  
>                   result = FSDK.GetFaceTemplateInRegion(picture, faceCoords, faceTemplate);  
>  
>                 if (result == FSDK.FSDKE_OK) {  
>                     // Here we send the face template found to matchFaces method which will compare the face template given with face templates in database to recognise the person.
>                     facesMatch = matchFaces(faceTemplate);  
>  
>                 } else {  
>                    Log.e(TAG, "Failed to get template");  
>                 }  
>            } else {  
>                Log.e(TAG, "Face not detected.");  
>                 }  
>        }  
>        return log;  
>  }  
>  
>    //It will set the image to the imageview with the rectangle around the face  
>  @Override  
>  protected void onPostExecute(String resultstring) {  
>    
>        if (result != FSDK.FSDKE_OK)  
>            return;  
>            
>         //Create a faceImageView to show the face picture     
>        FaceImageView imageView = (FaceImageView) findViewById(R.id.imageView);  
>        
>        // set the bitmap to the imageview
>        imageView.setImageBitmap(BitmapFactory.decodeFile(picturePath));  
>        
>        // get the face coordinates to draw a rectangle around the face
>        imageView.detectedFace = faceCoords;  
>        int[] realWidth = new int[1];  
>        FSDK.GetImageWidth(picture, realWidth);  
>        imageView.faceImageWidthOrig = realWidth[0];  
>        imageView.invalidate(); // redraw, to show rectangle marking up faces 
>  }
>```
2. The second process revolves around the comparison of the interfacial features stored in "SanadProject.db" database.
>
>After detecting the face and extracting the face features we will create a template for the face to store it and then send it to the method matchFaces to do the recognition part:-

> ```java
>public boolean matchFaces(FSDK.FSDK_FaceTemplate faceTemp) {  
>    // Get all face templates of all users from database with their ids
>    HashMap<Integer, FSDK.FSDK_FaceTemplate> patientsList = patientDAO.getAllPatientTemplates();  
>    HashMap<Integer, FSDK.FSDK_FaceTemplate> caregiversList = caregiverDAO.getAllCaregiverTemplates();  
>    HashMap<Integer, FSDK.FSDK_FaceTemplate> familyMembersList = familyMemberDAO.getAllFamilyMemberTemplates();  
>  
>    //Loop around the data inside each map
>    for (Map.Entry<Integer, FSDK.FSDK_FaceTemplate> patientsEntry : patientsList.entrySet()) {  
>    
>  	   //create a float variable to store the similarity of each each two templates
>        float SimilarityByReference[] = new float[1];  
>        
>        //Using the MatchFace function provided in FSDK we can find the probability of similarity
>        int result1 = FSDK.MatchFaces(faceTemp, patientsEntry.getValue(), SimilarityByReference);  
>        if (result1 == FSDK.FSDKE_OK) {  
>        
>            //If face templates match we will check how much is the similarity between them and based on it we decide the action such as below: 
>            float Similarity = SimilarityByReference[0];  
>            if (Similarity >= 0.95) {  
>            
>                // If the faces match and their similarity is higher than 0.95 then say the patient name and break out of the loop
>                Patient patient = patientDAO.getPatientById(patientsEntry.getKey());  
>                mCurrentPhotoPath = patient.getImagePath();  
>                say(qiContext, "This is " + patient.getName());  
>                return true;  
>             } else {  
>                Log.i(TAG, "Faces not match");  
>                 }  
>        } else if (result1 == FSDKE_UNSUPPORTED_TEMPLATE_VERSION) {  
>            Log.i(TAG, "Unsupported template");  
>        } else {  
>            Log.i(TAG, "Match failed");  
>          }  
>    }  
>    //if templates doesnt matchpepper will say the following phrase and it will return false 
>    sayAsync(qiContext, "Person Unknown");  
>  
>    return false;
> }
>```




