fovedit coalesced

original code - AspectRatioAxisConstraint=AspectRatio_MaintainXFOV

change code to - AspectRatioAxisConstraint=AspectRatio_MaintainYFOV

also 
this is the chase camera fov changes (fov when moving)
original code - m_useSpeedFoV=false

Change code to - m_useSpeedFoV=true
put fov  to m_speedFoVNewValue=120

this should give a wider fov similar to dmc4 

now i have to figure out to patch this without repackaging my whole game

coalesced_int.bin is the original for the international english
