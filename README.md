# Chatla SDK for Unity

A lightweight Unity SDK for sending events and managing user engagement via Chatla.

## Installation

### Unity Package Manager (recommended)

1. Open **Window > Package Manager**
2. Click **+** > **Add package from git URL...**
3. Paste:

```
https://github.com/Simply-Expert/chatla-unity.git?path=ChatlaSdk#v1.0.2
```

To update, change the version tag (e.g. `#v1.1.0`).

### Manual

Download the `.unitypackage` from [Releases](https://github.com/Simply-Expert/chatla-unity/releases) and import it into your project.

## Requirements

- Unity 2020.3+
- `com.unity.nuget.newtonsoft-json` (installed automatically via UPM)

## Quick Start

### 1. Initialize the SDK

Call `Chatla.Initialize()` once at app startup:

```csharp
using ChatlaSdk;

public class GameInit : MonoBehaviour
{
    void Start()
    {
        Chatla.Initialize("YOUR_API_KEY", "YOUR_SECRET", userId: "player_123");
    }
}
```

### 2. Identify a user (onboarding)

```csharp
Chatla.Identify("phone_number", tag: "vip");
// or
Chatla.UserOnboard("phone_number");
```

### 3. Send events

```csharp
using ChatlaSdk.Models;

// Typed convenience methods
Chatla.GameStart();
Chatla.LevelUp(playerLevel: 5);
Chatla.PurchaseAttempt(productId: "gem_pack_100");
Chatla.IapTransaction(productId: "gem_pack_100", isFirstPurchase: true);
Chatla.AchievementUnlocked(achievementId: "first_win");

// Or use the generic method with custom data
Chatla.SendEvent(ChatlaEventType.ItemAcquired, new Dictionary<string, object>
{
    { "item_id", "sword_01" },
    { "item_type", "weapon" }
});
```

### 4. Open messaging channels

```csharp
await Chatla.OpenWhatsappAsync();
await Chatla.OpenMessengerAsync();
```

### 5. User traits

```csharp
Chatla.SetTrait("vip_level", "gold");
Chatla.SetTraits(new Dictionary<string, object>
{
    { "country", "US" },
    { "signup_date", "2025-01-15" }
});
```

## Supported Events

| Event | Convenience Method |
|---|---|
| UserOnboard | `Identify()` / `UserOnboard()` |
| GameStart | `GameStart()` |
| LevelUp | `LevelUp()` |
| ConsecutiveFailures | `ConsecutiveFailures()` |
| PurchaseAttempt | `PurchaseAttempt()` |
| IapTransaction | `IapTransaction()` |
| ItemAcquired | `ItemAcquired()` |
| ItemSpent | `ItemSpent()` |
| AdComplete | `AdComplete()` |
| InactivityDetected | `InactivityDetected()` |
| Participation | `Participation()` |
| AchievementUnlocked | `AchievementUnlocked()` |
| NoPurchase | `NoPurchase()` |
| StoreOpened | `StoreOpened()` |
| TutorialSkipped | `TutorialSkipped()` |
| SessionEnd | `SessionEnd()` |

## GDPR / Privacy

```csharp
// Disable all tracking
Chatla.SetTrackingEnabled(false);

// Handle user data deletion request
Chatla.OnUserRequestedDeletion();
```

## Playground

The SDK includes a Playground component for testing events without writing code. In Unity go to **ChatlaSdk > Create Playground Prefab** to set it up in your scene.

## License

MIT License - see [LICENSE](LICENSE) for details.
