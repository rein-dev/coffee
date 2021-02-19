# coffee

package com.example.justjava;


import java.text.NumberFormat;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import android.view.View;
import android.widget.TextView;

/**
 * This app displays an order form to order coffee.
 */
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    int numberOfCoffees = 0;

    /**
     * This method is called when the order button is clicked.
     */
    public void submitOrder(View view) {
        if (numberOfCoffees == 0){
            String message = "Please place an order";
            displayMessage(message);
        }
        else{
            String priceMessage = "Your bill comes to R" + numberOfCoffees * 21;
            displayMessage(priceMessage);
        }

    }

    public void increment(View view){
        numberOfCoffees++;
        display(numberOfCoffees);
    }

    public void decrement(View view){
        numberOfCoffees--;
        if(numberOfCoffees <= 0){
            numberOfCoffees = 0;
        }
        display(numberOfCoffees);
    }

    /**
     * This method displays the given quantity value on the screen.
     */
    private void display(int number) {
        TextView quantityTextView = (TextView) findViewById(R.id.quantity_text_view);
        quantityTextView.setText("" + number);
    }
    /**
     * This method displays the given price on the screen.
     */
    private void displayPrice(int number) {
        TextView priceTextView = (TextView) findViewById(R.id.price_text_view);
        priceTextView.setText(NumberFormat.getCurrencyInstance().format(number));
    }

    /**
     * This method displays the given text on the screen.
     */
    private void displayMessage(String message) {
        TextView priceTextView = (TextView) findViewById(R.id.price_text_view);
        priceTextView.setText(message);
    }
}

-----------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:paddingBottom="16dp"
    android:paddingTop="16dp"
    android:paddingLeft="16dp"
    android:paddingRight="16dp"
    tools:context=".MainActivity"
    >


    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Quantity"
        android:layout_marginBottom="16dp"
        android:textAllCaps="true"
        />

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal">



            <Button
                android:layout_width="48dp"
                android:layout_height="48dp"
                android:text="-"
                android:onClick="decrement"
                />

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="0"
                android:id="@+id/quantity_text_view"
                android:layout_marginBottom="16dp"
                android:layout_marginLeft="16dp"
                android:layout_marginRight="16dp"
            />

            <Button
                android:layout_width="48dp"
                android:layout_height="48dp"
                android:text="+"
                android:onClick="increment"
                />

         </LinearLayout>

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Price"
        android:layout_marginTop="16dp"
        android:layout_marginBottom="16dp"
        />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/price_text_view"
        android:text="0"
        />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="order"
        android:layout_marginTop="16dp"
        android:onClick="submitOrder"
        />

</LinearLayout>
