# Hola_Luna
Simulacion Fisica de un objeto de carbono de tungsteno cayendo a una distancia de 15 mts a la Luna.

##Link Proyecto
https://github.com/JohnWickNesquik/Hola_Luna.git

##Conceptos

#Gravedad de la Luna
Es necesario conocer el dato para poder ajustar adecuadamente la simulacion, exactamente: 1.62 m/s^2, totalmente diferente a la que hay en la tierra la cual es 9,8 m/s. En conclusion podemos pesar unas 6 veces menos.

#Carburo de Tungsteno
Este tiene una densidad de 15.63 g/cm^3 que sera convertido a kg/m^3 osease 15600

#Agregamos un simbolo de "-" en la posicion y, para asegurarnos que el objeto caiga.



##Codigo
#include <iostream>
#include <Box2d/Box2d.h>


int main() {

//Se define la gravedad, en la luna.
    b2Vec2 gravity(0.0f, -1.623f);

    //Aqui definimos el mundo con la gravedad
    b2World world(gravity);

    //Se define el cuerpo y su posicion

    b2BodyDef groundBodyDef;
    groundBodyDef.position.Set(0.0f, -10.0f);

    //Se crea el cuerpo en el mundo

    b2Body *groundBody = world.CreateBody(&groundBodyDef);

//Se le da una forma de poligono y se posiciona junto a su radio.
    b2PolygonShape groundBox;
    groundBox.SetAsBox(50.0f, 10.0f);

    groundBody->CreateFixture(&groundBox, 0.0f);

    b2BodyDef bodyDef;
    bodyDef.type = b2_dynamicBody;
    // La posicion en metros.
    bodyDef.position.Set(0.0f, 15.0f);
    b2Body *body = world.CreateBody(&bodyDef);

    b2PolygonShape dynamicBox;
    dynamicBox.SetAsBox(1.0f, 1.0f);

//Fixture donde se le da la forma, densidad y friccion
    b2FixtureDef fixtureDef;
    fixtureDef.shape = &dynamicBox;
    // convierte gramos a kg/m^3
    fixtureDef.density = 15600.0f;
    fixtureDef.friction = 0.0f;
/Aqui se crea la fixture
    body->CreateFixture(&fixtureDef);


    float timeStep = 1.0f;

    int32 velocityIterations = 6;
    int32 positionIterations = 2;
//Aqui el for actualizara posicion por posicion el movimiento

    for (int32 i = 0; i < 15; ++i)
    {
        world.Step(timeStep, velocityIterations, positionIterations);
        b2Vec2 position = body->GetPosition();
        float angle = body->GetAngle();
        printf("%4.2f %4.2f %4.2f\n", position.x, position.y, angle);
    }
}


## En conclusion debemos manejar una sola medicion en general al hacer simulaciones de Fisica, en este caso fue en metros. Ademas tener los datos bien organizados en el caso de la gravedad de la luna, la densidad del Carburo de Tungsteno y la posicion en metros. Todo esto actualizable para que la simulacion pueda ser mas precisa y ver los numeros finales que van decrementando para hacer enfasis en la caida posicion por posicion.
