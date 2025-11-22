package com.example.c1_prak3_13020250206;

import androidx.appcompat.app.AppCompatActivity;
import android.content.res.ColorStateList;
import android.graphics.Color;
import android.os.Bundle;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    CheckBox chkCoto, chkSop, chkKetupat;
    EditText edtCoto, edtSop, edtKetupat;
    Button btnOK, btnReset;
    TextView txtTotal;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Inisialisasi komponen
        chkCoto = findViewById(R.id.chkCoto);
        chkSop = findViewById(R.id.chkSop);
        chkKetupat = findViewById(R.id.chkKetupat);

        edtCoto = findViewById(R.id.edtCoto);
        edtSop = findViewById(R.id.edtSop);
        edtKetupat = findViewById(R.id.edtKetupat);

        btnOK = findViewById(R.id.btnOK);
        btnReset = findViewById(R.id.btnReset);
        txtTotal = findViewById(R.id.txtTotal);

        // Warna untuk Checkbox (biru saat dicentang)
        ColorStateList checkBoxColor = new ColorStateList(
                new int[][]{
                        new int[]{-android.R.attr.state_checked},
                        new int[]{android.R.attr.state_checked}
                },
                new int[]{
                        Color.GRAY,
                        Color.parseColor("#00BCD4")
                }
        );

        chkCoto.setButtonTintList(checkBoxColor);
        chkSop.setButtonTintList(checkBoxColor);
        chkKetupat.setButtonTintList(checkBoxColor);

        // Default: nonaktifkan EditText
        setEditState(edtCoto, false);
        setEditState(edtSop, false);
        setEditState(edtKetupat, false);

        chkCoto.setOnCheckedChangeListener((b, checked) -> setEditState(edtCoto, checked));
        chkSop.setOnCheckedChangeListener((b, checked) -> setEditState(edtSop, checked));
        chkKetupat.setOnCheckedChangeListener((b, checked) -> setEditState(edtKetupat, checked));

        btnOK.setOnClickListener(v -> {
            int total = 0;
            if (chkCoto.isChecked()) total += getJumlah(edtCoto) * 13.000;
            if (chkSop.isChecked()) total += getJumlah(edtSop) * 20.000;
            if (chkKetupat.isChecked()) total += getJumlah(edtKetupat) * 1.000;
            txtTotal.setText("Total : Rp " + total);
        });

        // Tombol RESET
        btnReset.setOnClickListener(v -> {
            chkCoto.setChecked(false);
            chkSop.setChecked(false);
            chkKetupat.setChecked(false);

            edtCoto.setText("");
            edtSop.setText("");
            edtKetupat.setText("");

            txtTotal.setText("TOTAL");
        });
    }

    private void setEditState(EditText editText, boolean enabled) {
        editText.setEnabled(enabled);
        editText.setFocusable(enabled);
        editText.setFocusableInTouchMode(enabled);

        if (!enabled) {
            editText.setBackgroundTintList(ColorStateList.valueOf(Color.LTGRAY));
            editText.setHintTextColor(Color.LTGRAY);
        } else {
            editText.setBackgroundTintList(ColorStateList.valueOf(Color.LTGRAY)); // default abu
            editText.setHintTextColor(Color.DKGRAY);

            editText.setOnFocusChangeListener((v, hasFocus) -> {
                if (hasFocus) {
                    editText.setBackgroundTintList(ColorStateList.valueOf(Color.parseColor("#00BCD4"))); // garis bawah biru
                    editText.setHighlightColor(Color.parseColor("#00BCD4")); // warna seleksi teks
                } else {
                    editText.setBackgroundTintList(ColorStateList.valueOf(Color.LTGRAY)); // kembali abu
                }
            });
        }
    }
    // Fungsi ambil jumlah input
    private int getJumlah(EditText edt) {
        String val = edt.getText().toString();
        if (val.isEmpty()) return 0;
        else return Integer.parseInt(val);}}



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="#FFFFFF"
    android:padding="0dp">

       
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="#6200EE"
            android:padding="12dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Lat Input Control"
            android:textColor="#FFFFFF"
            android:textSize="18sp"
            android:textStyle="bold" />
    </LinearLayout>

   
    <LinearLayout
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:padding="16dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Menu :"
            android:textStyle="bold"
            android:textSize="16sp"
            android:layout_marginBottom="10dp" />

       
        <LinearLayout
            android:orientation="horizontal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center_vertical"
            android:layout_marginBottom="6dp">

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="1. Coto Makassar"
                android:textSize="15sp" />

            <CheckBox
                android:id="@+id/chkCoto"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content" />

            <TextView
                android:layout_width="80dp"
                android:layout_height="wrap_content"
                android:text="Rp 13.000"
                android:gravity="right"
                android:layout_marginLeft="5dp"
                android:textSize="15sp" />

            <EditText
                android:id="@+id/edtCoto"
                android:layout_width="50dp"
                android:layout_height="wrap_content"
                android:hint="JML"
                android:gravity="center"
                android:inputType="number"
                android:textSize="15sp"
                android:layout_marginLeft="5dp" />
        </LinearLayout>

       
        <LinearLayout
            android:orientation="horizontal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center_vertical"
            android:layout_marginBottom="6dp">

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="2. Sop Sodara"
                android:textSize="15sp" />

            <CheckBox
                android:id="@+id/chkSop"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content" />

            <TextView
                android:layout_width="80dp"
                android:layout_height="wrap_content"
                android:text="Rp 20.000"
                android:gravity="right"
                android:layout_marginLeft="5dp"
                android:textSize="15sp" />

            <EditText
                android:id="@+id/edtSop"
                android:layout_width="50dp"
                android:layout_height="wrap_content"
                android:hint="JML"
                android:gravity="center"
                android:inputType="number"
                android:textSize="15sp"
                android:layout_marginLeft="5dp" />
        </LinearLayout>

       
        <LinearLayout
            android:orientation="horizontal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center_vertical"
            android:layout_marginBottom="20dp">

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="3. Ketupat"
                android:textSize="15sp" />

            <CheckBox
                android:id="@+id/chkKetupat"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content" />

            <TextView
                android:layout_width="80dp"
                android:layout_height="wrap_content"
                android:text="Rp 1.000"
                android:gravity="right"
                android:layout_marginLeft="5dp"
                android:textSize="15sp" />

            <EditText
                android:id="@+id/edtKetupat"
                android:layout_width="50dp"
                android:layout_height="wrap_content"
                android:hint="JML"
                android:gravity="center"
                android:inputType="number"
                android:textSize="15sp"
                android:layout_marginLeft="5dp" />
        </LinearLayout>

        
        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="25dp">

            <Button
                android:id="@+id/btnOK"
                android:layout_width="120dp"
                android:layout_height="wrap_content"
                android:background="@drawable/btn_gray"
                android:elevation="40dp"
                android:text="OK"
                android:textColor="#000000"
                android:translationZ="7dp"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />

            <Button
                android:id="@+id/btnReset"
                android:layout_width="120dp"
                android:layout_height="wrap_content"
                android:layout_marginStart="16dp"
                android:background="@drawable/btn_gray"
                android:elevation="40dp"
                android:text="RESET"
                android:textColor="#000000"
                android:translationZ="7dp"
                app:layout_constraintBottom_toBottomOf="@+id/btnOK"
                app:layout_constraintStart_toEndOf="@+id/btnOK"
                app:layout_constraintTop_toTopOf="@+id/btnOK" />
        </androidx.constraintlayout.widget.ConstraintLayout>

        
        <TextView
            android:id="@+id/txtTotal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="TOTAL"
            android:textSize="28sp"
            android:textStyle="bold"
            android:gravity="center"
            android:textColor="#444444" />

    </LinearLayout>
</LinearLayout>
