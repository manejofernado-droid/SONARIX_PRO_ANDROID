package com.sonarix.pro

import android.Manifest
import android.bluetooth.BluetoothAdapter
import android.bluetooth.le.*
import android.content.pm.PackageManager
import android.os.*
import androidx.appcompat.app.AppCompatActivity
import android.widget.*
import androidx.core.app.ActivityCompat
import kotlin.math.pow

class MainActivity : AppCompatActivity() {

    private lateinit var status: TextView
    private lateinit var list: TextView
    private lateinit var radarView: RadarView
    private val lastRssi = mutableMapOf<String, Int>()
    private val bluetoothAdapter: BluetoothAdapter? by lazy {
        BluetoothAdapter.getDefaultAdapter()
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        status = findViewById(R.id.status)
        list = findViewById(R.id.list)
        radarView = findViewById(R.id.radarView)

        if (ActivityCompat.checkSelfPermission(
                this,
                Manifest.permission.ACCESS_FINE_LOCATION
            ) != PackageManager.PERMISSION_GRANTED
        ) {
            ActivityCompat.requestPermissions(
                this,
                arrayOf(Manifest.permission.ACCESS_FINE_LOCATION),
                1
            )
        }

        findViewById<Button>(R.id.scanBtn).setOnClickListener {
            startScan()
        }
    }

    private val scanCallback = object : ScanCallback() {
        override fun onScanResult(callbackType: Int, result: ScanResult) {
            val name = result.device.name ?: "Desconhecido"
            val rssi = result.rssi
            val distance = 10.0.pow(((-59) - rssi) / 20.0)
            val dir = when {
                !lastRssi.containsKey(name) -> "↕ Estável"
                rssi > lastRssi[name]!! + 3 -> "⬆ Aproximando"
                rssi < lastRssi[name]!! - 3 -> "⬇ Afastando"
                else -> "↕ Estável"
            }
            lastRssi[name] = rssi

            radarView.updateDevice(name, distance)
            list.text =
                "$name\nDistância: %.2f m\nRSSI: $rssi dBm\nMovimento: $dir".format(distance)
            status.text = "Dispositivo detectado"
        }
    }

    private fun startScan() {
        status.text = "Escaneando..."
        radarView.clearDevices()
        list.text = ""
        bluetoothAdapter?.bluetoothLeScanner?.startScan(null,
            ScanSettings.Builder().setScanMode(ScanSettings.SCAN_MODE_LOW_LATENCY).build(),
            scanCallback
        )
        Handler(Looper.getMainLooper()).postDelayed({
            bluetoothAdapter?.bluetoothLeScanner?.stopScan(scanCallback)
            status.text = "Scan ativo"
        }, 15000)
    }
}
package com.sonarix.pro

import android.content.Context
import android.graphics.*
import android.util.AttributeSet
import android.view.View
import kotlin.math.cos
import kotlin.math.sin
import kotlin.random.Random

class RadarView(context: Context, attrs: AttributeSet) : View(context, attrs) {

    private val paint = Paint()
    private val devices = mutableMapOf<String, Double>()

    fun updateDevice(name: String, distance: Double) {
        devices[name] = distance
        invalidate()
    }

    fun clearDevices() {
        devices.clear()
        invalidate()
    }

    override fun onDraw(canvas: Canvas) {
        super.onDraw(canvas)
        val cx = width / 2f
        val cy = height / 2f
        val radius = min(cx, cy) * 0.8f

        paint.style = Paint.Style.STROKE
        paint.color = Color.GRAY
        paint.strokeWidth = 4f
        canvas.drawCircle(cx, cy, radius, paint)

        paint.style = Paint.Style.FILL
        paint.color = Color.GREEN
        devices.forEach { (_, dist) ->
            val r = (dist / 8 * radius).toFloat().coerceAtMost(radius)
            val angle = Random.nextFloat() * 2 * Math.PI
            val x = cx + r * cos(angle).toFloat()
            val y = cy + r * sin(angle).toFloat()
            canvas.drawCircle(x, y, 12f, paint)
        }
    }
}
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:padding="20dp"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/status"
        android:text="SONARIX PRO"
        android:textSize="20sp"
        android:textStyle="bold"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <Button
        android:id="@+id/scanBtn"
        android:text="Iniciar Escaneamento"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"/>

    <com.sonarix.pro.RadarView
        android:id="@+id/radarView"
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:layout_gravity="center"
        android:layout_marginTop="20dp"/>

    <TextView
        android:id="@+id/list"
        android:textSize="16sp"
        android:layout_marginTop="20dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
</LinearLayout>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.sonarix.pro">

    <uses-permission android:name="android.permission.BLUETOOTH"/>
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
    <uses-permission android:name="android.permission.BLUETOOTH_SCAN"/>
    <uses-permission android:name="android.permission.BLUETOOTH_CONNECT"/>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

    <application
        android:allowBackup="true"
        android:label="SONARIX PRO"
        android:theme="@style/Theme.AppCompat.Light.NoActionBar">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
    </application>
</manifest>
