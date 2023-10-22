# Weekly Report 8 - 10/12/2023 - 10/19/2023

## Summary
This week, we successfully completed Project 2. In this project, we effectively utilized two Photon boards for signal transmission through the Particle web and employed Unity to read and display data via the serial port. We designed a mobile device capable of gathering information about the environment surrounding plants, and shaped the device using CAD modeling. Additionally, we crafted a 3D scene of a virtual garden in Unity to showcase plant models and environmental data.

Presentation Video Link: https://youtu.be/v1beZFs5Noo
   
## Unity / Photon 2 Code Update
**Photos:** <p>
<p align="center">
	<img width="900" alt="截屏2023-10-22 00 55 48" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/6718b2c8-3c24-4d27-9b68-200ea5714288">
</p>

<p align="center">
	<img width="900" alt="截屏2023-10-22 00 56 04" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/e01f2610-595a-4047-b645-7f9b1bc57e5f">
</p>

**Unity Code** </p>
**OnCollision**
```
using UnityEngine;

public class OnCollision : MonoBehaviour
{
    public GameObject ui_tree;
    public GameObject ui_blue;
    public GameObject ui_mushroom;
    public GameObject ui_grass;

    void OnTriggerEnter(Collider other)
    {

        if (other.CompareTag("tree"))
        {
            Debug.Log("on collision");
            ShowUI(ui_tree);
        }
        else if (other.CompareTag("blue"))
        {
            ShowUI(ui_blue);
        }
        else if (other.CompareTag("mushroom"))
        {
            ShowUI(ui_mushroom);
        }
        else if (other.CompareTag("grass"))
        {
            ShowUI(ui_grass);
        }
    }

    void ShowUI(GameObject ui)
    {
        ui.SetActive(true);
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.F))
        {
            HideAllUI();
        }
    }

    void HideAllUI()
    {
        ui_tree.SetActive(false);
        ui_blue.SetActive(false);
        ui_grass.SetActive(false);
        ui_mushroom.SetActive(false);
    }
}
```
**SerialRead**
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class SerialRead : MonoBehaviour
{
    public TMP_Text TreeText;
    public TMP_Text MushroomText;
    public TMP_Text BlueText;
    public TMP_Text GrassText;

    public GameObject vfx;

    public GameObject treeObject;
    public GameObject mushroomObject;
    public GameObject grassObject;
    public GameObject blueObject;
    
    private int a = 0;
    private GameObject plant;

    // Start is called before the first frame update
    void Start()
    {
        vfx.SetActive(false);
        treeObject.SetActive(false);
        mushroomObject.SetActive(false);
        grassObject.SetActive(false);
        blueObject.SetActive(false);
    }

    // Update is called once per frame
    void Update()
    {

    }

	//for List data
	public void ReadComplateList(object data)
	{
        var text = data as List<string>;

        //for (int i = 0; i < text.Count; ++i) {

        //    string[] values = text[i].Trim('[', ']').Split(',');
        
        //    if (values.Length == 2)
        //    {
        //        Debug.Log("Soil Moisture: " + values[0]);
        //        Debug.Log("Sunlight: " + values[1]);
        //       UpdateUI(values[0], values[1]);
        //    }
        //}

		for (int i = 0; i < text.Count; ++i) {
			Debug.Log(text[i]);  
            UpdateUI(text[i]); 

            if (int.Parse(text[i]) > 3000) {

                ++a;

                UpdatePlant();

                if (a == 5){
                    a = 0;
                }

                Debug.Log(a);
            }
        }
	}

    void UpdateUI(string value)
    {

        if (a == 1){
            TreeText.text = "Sunlight: " + value;
        }
        else if (a == 2){
            MushroomText.text = "Sunlight: " + value;
        }
        else if (a == 3){
            GrassText.text = "Sunlight: " + value;
        }
        else if (a == 4){
            BlueText.text = "Sunlight: " + value;
        }
        else {
            Debug.Log("out of range");
        }

        //displayText.text = "Sunlight: " + value;

    }


    void UpdatePlant()
    {
        if (a == 1){
            plant = treeObject;
        }
        else if (a == 2){
            plant = mushroomObject;
        }
        else if (a == 3){
            plant = grassObject;
        }
        else if (a == 4){
            plant = blueObject;
        }

        vfx.transform.position = plant.transform.position;
        vfx.SetActive(true);
        Invoke("ShowPlant", 2f);
        
    }

    void ShowPlant()
    {
        // Disable the VFX object
        vfx.SetActive(false);

        // Enable the plant object
        plant.SetActive(true);
    }

}
```
**Photon 2 Code** </p>
**Sender**
```
int soilMoisturePin = A0; // Soil Moisture Sensor pin
int sunlightPin = A1;     // Sunlight Sensor pin
int ledPin = D7;          // LED light pin

int soilMoistureValue;
int sunlightValue;

void setup() {
    Serial.begin(9600); //Initialize Serial
    
    Particle.variable("soilMoisture", soilMoistureValue);   
    Particle.variable("sunlight", sunlightValue);
    
    pinMode(ledPin, OUTPUT); 
}

void loop() {
    
    // Update sensor values
    soilMoistureValue = analogRead(soilMoisturePin);
    sunlightValue = analogRead(sunlightPin);
  
    Particle.publish("sensor_data", String(soilMoistureValue) + "," + String(sunlightValue));
    
    // Print data to serial port
    Serial.print("1-Soil Moisture: ");
    Serial.println(soilMoistureValue);
    Serial.print("1-Sunlight: ");
    Serial.println(sunlightValue);

    // Light up LED by conditions
    if (soilMoistureValue < 500 && sunlightValue > 600) {
        digitalWrite(ledPin, HIGH);
    } else {
        digitalWrite(ledPin, LOW);
    }

    delay(1000);

}
```
**Receiver**
```
int soilMoistureValue = 0;
int sunlightValue = 0;

void setup() {
    Serial.begin(9600);
    
    Particle.subscribe("sensor_data", onDataReceived);
}

void loop() {
    Serial.print("2-Soil Moisture: ");
    Serial.println(soilMoistureValue);
    Serial.print("2-Sunlight: ");
    Serial.println(sunlightValue);
    delay(1000);
}

void onDataReceived(const char *event, const char *data) {
    soilMoistureValue = atoi(strtok((char*)data, ","));
    sunlightValue = atoi(strtok(NULL, ","));
}
```


## Speculation
1. Due to sensor limitations, our prototype currently only displays two pieces of data related to plant growth: sunlight intensity and soil moisture. As a potential future development, we could integrate more sensors into the mobile device to gain a more comprehensive understanding of plant growth ecology.

2. We aim to incorporate machine learning algorithms to enable the function of capturing photos for plant type identification and generating corresponding 3D plant models within the scenes. We may achieve this by providing keywords through the algorithm to generate images in Midjourney, and then converting the model through an AI-driven picture processing method.

3. The current prototype exists as a Unity 3D scene. In the future, we aspire to enhance both the scene and its interactive elements into a VR format to further heighten the sense of immersion.
