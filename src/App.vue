<script setup lang="ts">
import { World, Model,FirstPersonCamera, Dummy, Find, Setup, keyboard, types } from "lingo3d-vue"
import { ref } from "vue"

const dummyRef = ref< types.Dummy >()

keyboard.onKeyPress = (key,pressed) =>{
  const dummy = dummyRef.value
  if (!dummy) return
  if (pressed.has("w"))
     dummy.strideForward  = -5
  if (pressed.has("s"))
     dummy.strideForward  = 5
  if (pressed.has("a"))
     dummy.strideRight  = 5
  if (pressed.has("d"))
     dummy.strideRight  = -5
}
keyboard.onKeyUp = (_,pressed) => {
  const dummy = dummyRef.value
  if (!dummy) return
  if (!pressed.has("w")&& !pressed.has("s"))
     dummy.strideForward  = 0
 
  if (!pressed.has("a")&& !pressed.has("d"))
      dummy.strideRight  = 0

}
keyboard.onKeyDown = (key) => {
  const dummy = dummyRef.value
  if (!dummy) return
  if (key == "Space")
     dummy.jump(10)
}



</script>

<template>
  <World>
    <LingoEditor />
    <Model
      :x="3.61"
      :y="29.12"
      :z="99.76"
      :width="471.9"
      :depth="460.28"
      :scale-x="50"
      :scale-y="50"
      :scale-z="50"
      src="dd.glb"
      physics="map"
    />
    <FirstPersonCamera
      :x="-191.71"
      :y="-549.12"
      :z="9634.71"
      :rotation-y="-10"
      :inner-z="0"
      mouse-control-mode="orbit"
      active
      mouse-control
      :inner-x ="-20"
      :inner-y ="80"
    >
      <Dummy
        :animations='{"idle":"https://unpkg.com/lingo3d-dummy@1.0.1/assets/rifle-idle.fbx","running":"https://unpkg.com/lingo3d-dummy@1.0.1/assets/rifle-running.fbx","runningBackwards":"https://unpkg.com/lingo3d-dummy@1.0.1/assets/rifle-running-backwards.fbx","jumping":"https://unpkg.com/lingo3d-dummy@1.0.1/assets/rifle-falling.fbx"}'
        animation="idle"
        pbr
        :x="-191.71"
        :y="-549.12"
        :z="9634.71"
        :width="20"
        :depth="20"
        :scale-x="2.5"
        :scale-y="2.5"
        :scale-z="2.5"
        :rotation-y="90"
        src="https://unpkg.com/lingo3d-dummy@1.0.1/assets/ybot.fbx"
        preset="rifle"
        stride-move
        ref="dummyRef"
        physics="character"
        
      >
        <Find name="mixamorigRightHand" :normal-scale='{"x":1,"y":1}'>
          <Model
            :x="-2411.99"
            :y="-384.82"
            :z="-252.61"
            :width="26.63"
            :height="100"
            :depth="277.87"
            :scale-x="36.09"
            :scale-y="36.09"
            :scale-z="36.09"
            :rotation-x="-159.36"
            :rotation-y="-84.12"
            :rotation-z="104.9"
            :rotation="104.9"
            src="a1.glb"
          />
        </Find>
      </Dummy>
    </FirstPersonCamera>
    <Setup />
  </World>

</template>


