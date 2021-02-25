# coffee

package com.example.justjava;


import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

import android.text.Editable;
import android.util.Log;
import android.view.View;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;


public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    int quantity = 0;

    public void increment(View view) {
        if (quantity == 100) {
            return;
        }
        quantity = quantity + 1;
        displayQuantity(quantity);
    }


    public void decrement(View view) {
        if (quantity == 0) {
            return;
        }
        quantity = quantity - 1;
        displayQuantity(quantity);
    }


    public void submitOrder(View view) {

        EditText nameField = (EditText) findViewById(R.id.name_field);
        Editable nameEditable = nameField.getText();
        String name = nameEditable.toString();

        CheckBox whippedCreamCheckBox = (CheckBox) findViewById(R.id.whipped_cream_checkbox);
        boolean hasWhippedCream = whippedCreamCheckBox.isChecked();

        CheckBox chocolateCheckBox = (CheckBox) findViewById(R.id.chocolate_checkbox);
        boolean hasChocolate = chocolateCheckBox.isChecked();

        int price = calculatePrice(hasWhippedCream, hasChocolate);

        String message = createOrderSummary(name, price, hasWhippedCream, hasChocolate);

        Intent intent = new Intent(Intent.ACTION_SENDTO);
        intent.setData(Uri.parse("mailto:")); // only email apps should handle this
        intent.putExtra(Intent.EXTRA_SUBJECT, "Coffee order for " + name);
        intent.putExtra(Intent.EXTRA_TEXT, message);
        if (intent.resolveActivity(getPackageManager()) != null) {
            startActivity(intent);
        }
    }


    private int calculatePrice(boolean addWhippedCream, boolean addChocolate) {
        int basePrice = 21;

        if (addWhippedCream) {
            basePrice = basePrice + 5;
        }

        if (addChocolate) {
            basePrice = basePrice + 7;
        }
        return quantity * basePrice;
    }

    private String createOrderSummary(String name, int price, boolean addWhippedCream, boolean addChocolate) {
        String priceMessage = "Name: "+ name;
        priceMessage += "\nWhipped cream added? " + addWhippedCream;
        priceMessage += "\nChocolate added? " + addChocolate;
        priceMessage += "\nNumber of coffees ordered: " + quantity;
        priceMessage += "\nPrice: R" + price;
        priceMessage += "\nThank You";
        return priceMessage;
    }

    private void displayQuantity(int numberOfCoffees) {
        TextView quantityTextView = (TextView) findViewById(R.id.quantity_text_view);
        quantityTextView.setText("" + numberOfCoffees);
    }
}


----------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:paddingBottom="16dp"
        android:paddingLeft="16dp"
        android:paddingRight="16dp"
        android:paddingTop="16dp">

        <EditText
            android:id="@+id/name_field"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="name"
            android:inputType="text"
            android:layout_marginBottom="16dp"/>

        <TextView
            android:text="Toppings"
            android:layout_height="wrap_content"
            android:layout_width="wrap_content"
            />

        <CheckBox
            android:id="@+id/whipped_cream_checkbox"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:paddingLeft="24dp"
            android:text="whipped cream"
            android:textSize="16sp" />

        <CheckBox
            android:id="@+id/chocolate_checkbox"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:paddingLeft="24dp"
            android:text="chocolate"
            android:textSize="16sp" />

        <TextView
            android:layout_height="wrap_content"
            android:layout_width="wrap_content"
            android:text="Quantity" />

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <Button
                android:layout_width="48dp"
                android:layout_height="48dp"
                android:onClick="decrement"
                android:text="-" />

            <TextView
                android:id="@+id/quantity_text_view"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:paddingLeft="8dp"
                android:paddingRight="8dp"
                android:text="0"
                android:textColor="@android:color/black"
                android:textSize="16sp" />

            <Button
                android:layout_width="48dp"
                android:layout_height="48dp"
                android:onClick="increment"
                android:text="+" />

        </LinearLayout>

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="16dp"
            android:onClick="submitOrder"
            android:text="Order" />

    </LinearLayout>
</ScrollView>


