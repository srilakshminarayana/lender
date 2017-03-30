# lender 
Activity-main.xml 
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:background="#6fa9a1"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.personal.yamyah.MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="user name"
        android:textSize="15sp"
        android:textStyle="bold"
        android:id="@+id/textView" />


    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="textPersonName"
        android:hint="enter user name"
        android:ems="10"
        android:layout_alignParentTop="true"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true"
        android:id="@+id/editText2" />

    <TextView
        android:text="password"
        android:textSize="15sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/editText2"
        android:layout_alignRight="@+id/textView"
        android:layout_alignEnd="@+id/textView"
        android:layout_marginTop="59dp"
        android:id="@+id/textView3" />

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="textPersonName"
        android:hint="enter password"
        android:ems="10"
        android:layout_below="@+id/editText2"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true"
        android:layout_marginRight="22dp"
        android:layout_marginEnd="22dp"
        android:layout_marginTop="44dp"
        android:id="@+id/editText3" />

    <Button
        android:text="REgister"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#a49d9d"
        android:textColor="#101010"
        android:onClick="button"
        android:layout_centerVertical="true"
        android:layout_alignLeft="@+id/editText2"
        android:layout_alignStart="@+id/editText2"
        android:id="@+id/button" />

    <TextView
        android:text="Already register ? sign in here "

        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/button"
        android:layout_marginTop="74dp"
        android:id="@+id/textViewsignin"
        android:textAlignment="center"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true"
        android:layout_alignLeft="@+id/textView3"
        android:layout_alignStart="@+id/textView3" />

</RelativeLayout>

Main activity
package com.example.personal.yamyah;

import android.app.ProgressDialog;
import android.support.annotation.NonNull;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.text.TextUtils;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ProgressBar;
import android.widget.TextView;
import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    private Button signup;
    private EditText email;
    private EditText password;
    private TextView already;
    private FirebaseAuth firebaseauth;

    private ProgressDialog progressdialog;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        progressdialog = new ProgressDialog(this);
        firebaseauth = FirebaseAuth.getInstance();

        signup = (Button) findViewById(R.id.button);
        email = (EditText) findViewById(R.id.editText2);
        password = (EditText) findViewById(R.id.editText3);
        already = (TextView) findViewById(R.id.textViewsignin);
        signup.setOnClickListener(this);
        signup.setOnClickListener(this);
        email.setOnClickListener(this);
        password.setOnClickListener(this);
    }

    private void registeruser() {
        String email1 = email.getText().toString().trim();
        String password1 = password.getText().toString().trim();
        if (TextUtils.isEmpty(email1)) {
            //should not be empty
            Toast.makeText(this, "enter mail id", Toast.LENGTH_SHORT).show();
            return;
        }
        if (TextUtils.isEmpty(password1)) {
            //should not be empty
            Toast.makeText(this, "enter password", Toast.LENGTH_SHORT).show();
            return;
        }
        progressdialog.setMessage("registering user");
        progressdialog.show();

        firebaseauth.createUserWithEmailAndPassword(email1, password1)
                .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
                    @Override
                    public void onComplete(@NonNull Task<AuthResult> task) {
                        if (task.isSuccessful()) {
                            Toast.makeText(MainActivity.this, "registered successfully", Toast.LENGTH_SHORT).show();
                            Toast.makeText(MainActivity.this, " cannot registered ,please try again", Toast.LENGTH_SHORT).show();
                        }
                    }
                });

    }

    @Override
    public void onClick(View v) {
        if (v == signup) {
            registeruser();
        }
        if (v == already) {
        }
    }
}





