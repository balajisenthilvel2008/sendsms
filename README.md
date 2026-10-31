
# Ex.No:3 Design an android application Send SMS using Intent.


## AIM:

To create and design an android application Send SMS using Intent using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as smsintent and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Send SMS and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to create and design an android application Send SMS using Intent.
Developed by: BALAJI S
Registration Number : 212225220015
*/
```

### MainActivity.java

```
package com.example.exp3;

import android.os.Bundle;
import android.telephony.SmsManager;

import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import android.view.View;
import android.Manifest;
import android.content.pm.PackageManager;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;



public class MainActivity extends AppCompatActivity {

    EditText phone,message;
    Button send;

    private static final int SMS_PERMISSION_CODE=101;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        phone = findViewById(R.id.phone);
        message=findViewById(R.id.message);
        send=findViewById(R.id.send);

        send.setOnClickListener(new View.OnClickListener(){
            public void onClick(View v){
                String number=phone.getText().toString();
                String msg=message.getText().toString();
                if(number.isEmpty() || msg.isEmpty()){
                    Toast.makeText(MainActivity.this,"Enter Phone number and Message",Toast.LENGTH_SHORT).show();
                    return;
                }
                if(ContextCompat.checkSelfPermission(
                        MainActivity.this,
                        Manifest.permission.SEND_SMS)!=PackageManager.PERMISSION_GRANTED){
                    ActivityCompat.requestPermissions(MainActivity.this,
                            new String[]{Manifest.permission.SEND_SMS},
                            SMS_PERMISSION_CODE);
                }
                else{
                    sendSMS(number,msg);
                }

            }
        });

    }
    private void sendSMS(String number,String msg){
        try{
            SmsManager smsManager=getSystemService(SmsManager.class);
            smsManager.sendTextMessage(number,null,msg,null,null);
            Toast.makeText(this,"SMS sent successfully",Toast.LENGTH_SHORT).show();
        }
        catch(Exception e){
            Toast.makeText(this,"SMS sending failed"+e.getMessage(),Toast.LENGTH_LONG).show();
        }
    }
    @Override
    public void onRequestPermissionsResult(
            int requestCode,
            String[] permissions,
            int[] grantResults) {

        super.onRequestPermissionsResult(
                requestCode, permissions, grantResults);

        if (requestCode == SMS_PERMISSION_CODE) {

            if (grantResults.length > 0 &&
                    grantResults[0] == PackageManager.PERMISSION_GRANTED) {

                Toast.makeText(this, "Permission Granted",
                        Toast.LENGTH_SHORT).show();

                String number = phone.getText().toString().trim();
                String msg = message.getText().toString().trim();

                sendSMS(number, msg);

            } else {
                Toast.makeText(this, "SMS permission denied",
                        Toast.LENGTH_SHORT).show();
            }
        }
    }
}
```

### activity_main.xml

```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FF00F2"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="104dp"
        android:fontFamily="serif"
        android:text="Exp 3 "
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="40dp"
        android:fontFamily="serif"
        android:text="Enter Phone Number :"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.496"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView" />

    <EditText
        android:id="@+id/phone"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="44dp"
        android:ems="10"
        android:inputType="text"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView2" />

    <TextView
        android:id="@+id/textView3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="48dp"
        android:fontFamily="serif"
        android:text="Enter Message:"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/phone" />

    <EditText
        android:id="@+id/message"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="40dp"
        android:ems="15"
        android:inputType="text"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.494"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView3" />

    <Button
        android:id="@+id/send"
        style="@style/Widget.AppCompat.Button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Send"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/message"
        app:layout_constraintVertical_bias="0.181" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

### AndroidManifest.xml

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
    <uses-permission android:name="android.permission.SEND_SMS"/>
    <uses-feature
        android:name="android.hardware.telephony"
        android:required="false"/>
    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Exp3">
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:windowSoftInputMode="adjustResize">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```


## OUTPUT:

<img width="1920" height="1020" alt="Screenshot 2026-10-31 115720" src="https://github.com/user-attachments/assets/fb77820e-d997-4368-a546-82c4cb0d8942" />
<br>
<img width="1920" height="1020" alt="Screenshot 2026-10-31 115356" src="https://github.com/user-attachments/assets/cafd6ac3-ecbf-4e8c-a8f9-2f42b5bdf71b" />
<br>
<img width="1920" height="1020" alt="Screenshot 2026-10-31 115409" src="https://github.com/user-attachments/assets/8a01cf44-d363-4c9c-af11-636c689d3e47" />
<br>
<img width="1920" height="1020" alt="Screenshot 2026-10-31 115418" src="https://github.com/user-attachments/assets/fc1464b9-0092-4bdd-9e3e-b974726f75e8" />
<br>
<img width="1920" height="1020" alt="Screenshot 2026-10-31 115441" src="https://github.com/user-attachments/assets/59936760-5979-46b7-8f86-9bff87472e54" />
<br>
<img width="1920" height="1020" alt="Screenshot 2026-10-31 115619" src="https://github.com/user-attachments/assets/94546c42-f55f-47b6-942b-be61b5f9f18c" />


## RESULT
Thus a Simple Android Application create and design an android application Send SMS using Intent using Android Studio is developed and executed successfully.
