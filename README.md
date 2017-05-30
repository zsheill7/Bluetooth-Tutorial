In this tutorial, we're going to learn how to use Bluetooth in our Android apps.  

Bluetooth is becoming increasingly popular in smart homes and smart devices. You can use it to connect your device to a smart watch, earphones, or another home appliance.


<h1></h1>
Let's first create a new project.  I'm going to call mine BluetoothDemo.  Unfortunately, you can't use Bluetooth on the simulator, but if you have an Android phone, you can connect it to your computer and run the code on your phone.  

The first thing we will need to include is our BluetoothAdapter variable BA.  This allows us to work with Bluetooth.  

First, we need to see if the user has Bluetooth turned on.  

Use the .isEnabled() method to check if Bluetooth is enabled.  If it is, you can make a toast that tells the user that Bluetooth is on on their device. 

```
BluetoothAdapter BA;


    public void turnBluetoothOff (View view) {

        BA.disable();

        if (BA.isEnabled()) {

            Toast.makeText(getApplicationContext(), "Bluetooth could not be disabled", Toast.LENGTH_LONG).show();

        } else {

            Toast.makeText(getApplicationContext(), "Bluetooth turned off", Toast.LENGTH_LONG).show();

        }


    }
```


We also have to include permission for Bluetooth in our AndroidManifest.xml file.

```
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```

We need to create an intent to go to our Bluetooth Adapter.  We will use ACTION_REQUEST_ENABLE to enable Bluetooth.

We then do another check to see if Bluetooth enabled, and then tell the user it is turned on. 

```
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        if (BA.isEnabled()) {

            Toast.makeText(getApplicationContext(), "Bluetooth is on", Toast.LENGTH_LONG).show();

        } else {

            Intent i = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
            startActivity(i);

            if (BA.isEnabled()) {

                Toast.makeText(getApplicationContext(), "Bluetooth turned on", Toast.LENGTH_LONG).show();

            }

        }

    }
```


In our layout file, let's bring in a few buttons.

The first will be to turn Bluetooth off. 

The second will find nearby devices, such as earbuds or watches. 

Our third button will let us view paired devices (ones that are already paired with the phone)

Don't forget to set IDs for all three buttons.

Then, we need to set onClick methods for all three buttons.  

In MainActivity, we'll create the function "turnBluetoothOff"



We then need to add the permission to control Bluetooth. We will then check to see if Bluetooth is still enabled.  

Next, let's add an onClick for "findDiscoverableDevices"

This will go to a different intent.  

Next let's add an onClick for "view Paired Devices":

We need a Set, which is quite similar to a List, which we will call pairedDevices.  

We want to use an arrayAdapter to display the paired devices on our listView.  Let's create an ArrayList and call it pairedDevicesArrayList.  

Let's create a for loop to find Bluetooth devices from our pairedDevices Set.  For each of the devices, we will get the name and add its name to our pairedDevicesArrayList.  

    BluetoothAdapter BA;


    public void turnBluetoothOff (View view) {

        BA.disable();

        if (BA.isEnabled()) {

            Toast.makeText(getApplicationContext(), "Bluetooth could not be disabled", Toast.LENGTH_LONG).show();

        } else {

            Toast.makeText(getApplicationContext(), "Bluetooth turned off", Toast.LENGTH_LONG).show();

        }


    }

    public void findDiscoverableDevices (View view) {

        Intent i = new Intent(BluetoothAdapter.ACTION_REQUEST_DISCOVERABLE);
        startActivity(i);


    }

    public void viewPairedDevices (View view) {

        Set<BluetoothDevice> pairedDevices = BA.getBondedDevices();

        ListView pairedDevicesListView = (ListView) findViewById(R.id.pairedDevicesListView);

        ArrayList pairedDevicesArrayList = new ArrayList();

        for (BluetoothDevice bluetoothDevice : pairedDevices) {

            pairedDevicesArrayList.add(bluetoothDevice.getName());

        }

        ArrayAdapter arrayAdapter = new ArrayAdapter(this, android.R.layout.simple_list_item_1, pairedDevicesArrayList);

        pairedDevicesListView.setAdapter(arrayAdapter);

    }


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        if (BA.isEnabled()) {

            Toast.makeText(getApplicationContext(), "Bluetooth is on", Toast.LENGTH_LONG).show();

        } else {

            Intent i = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
            startActivity(i);

            if (BA.isEnabled()) {

                Toast.makeText(getApplicationContext(), "Bluetooth turned on", Toast.LENGTH_LONG).show();

            }

        }

    }