extends CharacterBody2D

var velocidad := 200
var salto := 225
var Camara_Lenta = false
@onready var AnimatedSprite2D = $animaciones


func _physics_process(delta):
	var direcion = Input.get_axis("ui_left", "ui_right")#Inicio de codigo de movimiento
	velocity.x = direcion * velocidad
	if is_on_floor() and Input.is_action_just_pressed("ui_up"):
		velocity.y -=  salto
	velocity.y += General.gravedad
	move_and_slide()#Fin del codigo de movimiento
 

if velocity.x !=0:#Inicio de codigo de animaciones 
		Animaciones_Jugador.play("Run")
	else:
		Animaciones_Jugador.play("Idle")
  
if not is_on_floor():
 Animaciones_Jugador.play("Jump")
 
if velocity.x !=0:
 Animaciones_Jugador.flip_h = direcion <0#fin de codigo de animaciones
 

if Camara_Lenta:
	if Engine.time_scale > 0.1:
		Engine.time_scale -= 5 * delta
	else:
		Engine.time_scale = 0.1 
else:
	if Engine.time_scale < 1:
		Engine.time_scale += 5 * delta
	else:
		Engine.time_scale = 1


func _input(_event):
if Input.is_action_just_pressed("ui_accept"): 
	Camara_Lenta = true 
	
 if Input.is_action_just_pressed("ui_cancel"):
  Camara_Lenta = false
