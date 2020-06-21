# Gunes-Sstem-Yorunge-simulasyn-Unity-Grupno24
unity içinde GüneşSistemiYörünge simülasonu csharp kodu ile formule dayalı oluşturma ve gözlemleme. Grupno24.
github destopla unity içindeki proje dosyaları yüklenmiştir.
temel c sharp kodu:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class Orbitters : MonoBehaviour {      
public int sphereCount = 500;
public int maxRadius = 200; 
public GameObject [] spheres;
public Material [] mats; 
public Material trailMat;
void Awake () {
spheres = new GameObject[sphereCount]; 
}          
void Start() {
spheres = CreateSpheres(sphereCount , maxRadius);  
}      
public GameObject [] CreateSpheres ( int count , int radius) 
{
var sphs=  new GameObject[count];
var sphereToCopy =  GameObject.CreatePrimitive (PrimitiveType.Sphere);      
Rigidbody rb =  sphereToCopy.AddComponent<Rigidbody>();
rb.useGravity = false;    
for (int i=0;  i < count;  i++)        
     {  
      var sp = GameObject. Instantiate( sphereToCopy ); 
      sp.transform.position  =  this.transform.position  +  

                                                 New Vector3( Random.Range ( - maxRadius , maxRadius ),         
                                                                         Random.Range (-10,10),
                                                                         Random.Range ( - maxRadius , maxRadius ) );

      sp.transform.localScale *= Random.Range ( 0.5f ,1 ) ;
      sp.GetComponent  <Renderer> ( ).material = mats [ Random.Range (0 , mats.Length) ] ;

      TrailRenderer tr  = sp.AddComponent <TrailRenderer> ( ) ;
      tr.time = 1.0f;     
      tr.startWidth = 0.1f; 
      tr.endWidth =0;
      tr.material = trailMat; 
      tr.startColor = new Color ( 1 ,1 ,0 ,0.1f ) ;
      tr.endColor = new Color ( 0 , 0 , 0 ,0 ) ;
      spheres [i] = sp ;     
}
GameObject.Destroy (sphereToCopy) ;    
return spheres ;   
}      
Void update () {  
foreach (GameObject s in spheres)
{  
   Vector3 difference  =  this.transform.position - s.transform.position ; 
   float dist  =  difference .magnitude;
   Vector3 gravityDirection  = difference.normalized; 
   float gravity  =  6.7f *  (this.transform.localScale.x *s.transform. localScale.x *80) 
     / (dist*dist); 
    Vector3 gravityVector  =  (gravityDirection * gravity); 
s.transform.GetComponent<Rigidbody> ().AddForce(s.transform.forward, 
ForceMode.Acceleration); 
s.transform.GetComponent<Rigidbody> ().AddForce(gravityVector, 
ForceMode.Acceleration);   
}  
}
} 
