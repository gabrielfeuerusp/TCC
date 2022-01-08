# Definir aplicacao
app = getApplication()

# Definir componentes
comp = getComponent()
base = app.findComponent("Base")

# Definir Servos
Servo_Esteira = comp.findBehaviour("Servo_Esteira")
Servo_Elevador = comp.findBehaviour("Servo_Elevador")
Servo_Garra = comp.findBehaviour("Servo_Garra")

# Definir sinais de comando
DO0 = comp.findBehaviour("DO0")
DO1 = comp.findBehaviour("DO1")
DO2 = comp.findBehaviour("DO2")
DO3 = comp.findBehaviour("DO3")
DO7 = comp.findBehaviour("DO7")

# Definir sinais de saida
DI0 = comp.findBehaviour("Sensor_Disponivel")
DI1 = comp.findBehaviour("Sensor_Buffer")
DI2 = comp.findBehaviour("Sensor_Prox_Est")
DI3 = comp.findBehaviour("Sensor_Rampa")
DI4 = comp.findBehaviour("Sensor_Garra_Avan")
DI5 = comp.findBehaviour("Sensor_Garra_Recu")
DI6 = comp.findBehaviour("Sensor_Cor")
DI7 = False

def OnRun():

  #identifica situacao da garra
  compeca = False
  
  while app.Simulation.IsRunning:
  
    # Peca entra no buffer
    if DO7.Value == False:
      Servo_Esteira.setJointTarget(1,-100.0)
      Servo_Esteira.move()
    
    # Abre garra
    if DO3.Value == True:
      compeca = False
      Servo_Garra.moveJoint(0,0.0)
    
    # Avanca garra
    if DO2.Value == True:
    
      # Para movimentacao da peca de trabalho
      if compeca == True:
        Servo_Elevador.setJointTarget(0,-104.2)
        Servo_Elevador.setJointTarget(1,0.0)
        Servo_Elevador.move()
        
      # Para movimentacao apenas da garra
      elif compeca == False:
        Servo_Elevador.setJointTarget(0,-104.2)
        Servo_Elevador.move()
    
    # Fecha garra
    if DO3.Value == False:
      compeca = True
      Servo_Garra.moveJoint(0,2.3)
    
    # Retrai garra
    if DO2.Value == False:
    
      # Para movimentacao apenas da garra
      if compeca == False:
        Servo_Elevador.setJointTarget(0,0.0)
        Servo_Elevador.move()
        
      # Para movimentacao da peca de trabalho
      elif compeca == True:
        Servo_Elevador.setJointTarget(0,0.0)
        Servo_Elevador.setJointTarget(1,104.2)
        Servo_Elevador.move()
    
    # Move modulo para proxima estacao
    if DO0.Value == True:
    
      # Se esta no buffer mover para rampa
      if DI6.BoolSignal.Value == False:
        Servo_Esteira.setJointTarget(0,-188.7)
        Servo_Esteira.setJointTarget(1,-288.7)
        Servo_Esteira.move()
        
      # Se esta na rampa mover para proxima estacao
      elif DI6.BoolSignal.Value == True:
        Servo_Esteira.setJointTarget(0,-352.2)
        Servo_Esteira.setJointTarget(1,-452.2)
        Servo_Esteira.move()
    
    # Recua modulo para estacao anterior
    if DO1.Value == True:
    
      # Se esta na proxima estacao mover para rampa
      if DI2.BoolSignal.Value == True:
        Servo_Esteira.setJointTarget(0,-188.7)
        Servo_Esteira.move()
        
      # Se esta na rampa mover para buffer
      elif DI3.BoolSignal.Value == True:
        Servo_Esteira.setJointTarget(0,0.0)
        Servo_Esteira.move()
    
  pass
