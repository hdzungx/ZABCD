# ViPER4Android FX

#### * **Works only on Android-14**
#### * **Use branch => <a href="https://gitlab.com/anandhan07/packages_apps_ViPER4AndroidFX/-/tree/master?ref_type=heads" target="blank">**master**</a> for Android-13 & lower support**

- Add this in **device.mk**:
```
    $(call inherit-product, packages/apps/ViPER4AndroidFX/config.mk)
```
- Add this to your **audio_effects.xml**:
```
    <library name="v4a_fx" path="libv4a_fx.so"/>
    <effect name="v4a_standard_fx" library="v4a_fx" uuid="41d3c987-e6cf-11e3-a88a-11aba5d5c51b"/>
```
- Also you need to address some SELinux denials in

**audioserver.te**:
```    
    allow audioserver unlabeled:file { read write open getattr };
    get_prop(audioserver, vendor_audio_prop)
```
**hal_audio_default.te**:
```    
    allow hal_audio_default hal_audio_default:process { execmem };
    get_prop(hal_audio_default, vendor_audio_prop)
    set_prop(hal_audio_default, vendor_audio_prop)
```
