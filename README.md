
# Ex.No:3 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “ex.no.3″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the text create your own content providers to get contacts details.
Developed by: TAMILSELVI P
Registeration Number : 212225040460
*/
```
## MainActivity.java:
```

package com.example.contactsprovider;

import android.Manifest;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity {

    Button getContacts;
    TextView contactDetails;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        getContacts = findViewById(R.id.getContacts);
        contactDetails = findViewById(R.id.contactDetails);

        getContacts.setOnClickListener(v -> {
            if (ContextCompat.checkSelfPermission(this,
                    Manifest.permission.READ_CONTACTS)
                    != PackageManager.PERMISSION_GRANTED) {

                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.READ_CONTACTS}, 1);

            } else {
                displayContacts();
            }
        });
    }

    @Override
    public void onRequestPermissionsResult(int requestCode,
                                           String[] permissions, int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        if (requestCode == 1 && grantResults.length > 0
                && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
            displayContacts();
        } else {
            Toast.makeText(this, "Permission Denied",
                    Toast.LENGTH_SHORT).show();
        }
    }

    private void displayContacts() {

        StringBuilder contacts = new StringBuilder();

        Cursor cursor = getContentResolver().query(
                ContactsContract.CommonDataKinds.Phone.CONTENT_URI,
                null, null, null,
                ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME + " ASC");

        if (cursor != null) {
            while (cursor.moveToNext()) {

                String name = cursor.getString(
                        cursor.getColumnIndexOrThrow(
                                ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME));

                String number = cursor.getString(
                        cursor.getColumnIndexOrThrow(
                                ContactsContract.CommonDataKinds.Phone.NUMBER));

                contacts.append("Name: ").append(name)
                        .append("\nPhone: ").append(number)
                        .append("\n\n");
            }
            cursor.close();
        }

        if (contacts.length() == 0) {
            contactDetails.setText("No contacts found");
        } else {
            contactDetails.setText(contacts.toString());
        }
    }
}

```
## activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Contact Details"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:padding="10dp"/>

    <Button
        android:id="@+id/getContacts"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Get Contacts"/>

    <TextView
        android:id="@+id/contactDetails"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="18sp"
        android:padding="10dp"/>

</LinearLayout>

```

## OUTPUT
<img width="1920" height="1080" alt="Screenshot (276)" src="https://github.com/user-attachments/assets/df6f967a-8917-4ab0-bc6b-5c8077032c9e" />

<img width="1920" height="1080" alt="Screenshot (277)" src="https://github.com/user-attachments/assets/7af2c1ca-6a5c-4214-89df-366f18ef868f" />

<img width="1920" height="1080" alt="Screenshot (278)" src="https://github.com/user-attachments/assets/c6a95eb9-e1e4-427a-86d5-6c00ad6d6731" />

<img width="1920" height="1080" alt="Screenshot (279)" src="https://github.com/user-attachments/assets/b55b5ad3-58d2-46fd-9955-b6c782ef79bc" />

## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
