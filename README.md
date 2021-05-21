# fortnite
Offsets and Sigs for your pasted cheat.
# Offsets
```
Uworld: 0x95405C0
GoObject: 0x9246BC0
Levels: 0x138
PersistentLevel: 0x30
LocalPlayers: 0x38
OwningGameInstance: 0x180
PlayerCameraManager: 0x2B8
AcknowledgedPawn: 0x2A0
PlayerState: 0x240
RootComponent: 0x130
Mesh: 0x280
RelativeLocation: 0x11C
ComponentVelocity: 0x140
StaticMesh: 0x4A8
CustomTimeDilation: 0x98
LastFireTimeVerified: 0x910
LastFireTime: 0x90C
bIsDBNO: 0x56E
bIsDying: 0x540
TeamIndex: 0xED0
PrimaryPickupItemEntry: 0x2A8
DisplayName: 0x88
Tier: 0x6C
ItemDefinition: 0x18
CurrentWeapon: 0x5F0
WeaponData: 0x378
LastFireAbilityTime: 0xB58
WeaponStatHandle: 0x820
FireStartLoc: 0x878
bAlreadySearched: 0xC81
RemoteViewPitch: 0x232
Spread: 0x15C
SpreadDownsights: 0x160
```
# Sigs
``` 
GoObject: 48 8B 05 ? ? ? ? 48 8B 0C C8 48 8B 04 D1
FnFree: 48 85 C9 0F 84 ? ? ? ? 53 48 83 EC 20 48 89 7C 24 30 48 8B D9 48 8B 3D ? ? ? ? 48 85 FF 0F 84 ? ? ? ? 48 8B 07 4C 8B 40 30 48 8D 05 ? ? ? ? 4C 3B C0
Uworld: 48 8B 05 ? ? ? ? 4D 8B C2
GetObjectName: 48 89 5C 24 ? 55 56 57 48 8B EC 48 83 EC ? 48 83 65 ? ? 49 8B F0 48 8B DA E8 ? ? ? ? 48 8B 43 ? 48 85 C0
ProjectionMatrixGivenView: E8 ? ? ? ? 41 88 07 48 83 C4 30
FNamePool: 48 8B 1D ? ? ? ? 48 03 C0
GetBoneMatrix: E8 ? ? ? ? F3 0F 10 48 38
LineOfSightTo: E8 ? ? ? ? 48 8B 0D ? ? ? ? 33 D2 40 8A F8
GetObjectName: instead of this sig use the function below


std::string GetObjectName(uintptr_t Object) {
 
            static uintptr_t addr = 0;
 
            if (!addr) {
                addr = FindPattern(xorstr("\x48\x89\x5C\x24\x00\x48\x89\x74\x24\x00\x55\x57\x41\x56\x48\x8D\xAC\x24\x00\x00\x00\x00\x48\x81\xEC\x00\x00\x00\x00\x48\x8B\x05\x00\x00\x00\x00\x48\x33\xC4\x48\x89\x85\x00\x00\x00\x00\x45\x33\xF6\x48\x8B\xF2\x44\x39\x71\x04\x0F\x85\x00\x00\x00\x00\x8B\x19\x0F\xB7\xFB\xE8\x00\x00\x00\x00\x8B\xCB\x48\x8D\x54\x24"), xorstr("xxxx?xxxx?xxxxxxxx????xxx????xxx????xxxxxx????xxxxxxxxxxxx???xxxxxx????xxxxxx"); //GetNameByIndex sig
                if (!addr) {
                    MessageBoxA((HWND)0, (LPCSTR)_("Failed to get GetNameByIndex"), (LPCSTR)0, (UINT)0);
                    exit(0);
                }
            }
 
            if (Object == NULL)
                return _("");
 
            auto fGetObjName = reinterpret_cast<FString * (__fastcall*)(int* index, FString* res)>(addr);
 
            int index = *(int*)(Object + 0x18);
 
            FString result;
            fGetObjName(&index, &result);
 
            if (result.c_str() == NULL)
                return _("");
 
            auto result_str = result.ToString();
 
            if (result.c_str() != NULL)
                Free((__int64)result.c_str());
 
            return result_str;
        }

```

If it isn't working just replace ? with 00 and before every part add \x
f.e: 
Before -> cpp 48 8B 0D ? ? ? ? 48 98 
After -> cpp \x48\x8B\x0D\x00\x00\x00\x00\x48\x98

# Credits: damo#7883 / Android#1336
