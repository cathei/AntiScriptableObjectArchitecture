# Anti ScriptableObject Architecture
❌ **DO NOT USE ScriptableObject Architecture** ❌

There is an outburst of abusing ScriptableObject in the wrong, wrong way. Including using it as Event Broker or Reactive variable. DO NOT DO THIS. Don't even think about it. I've collected many reasons to stop this madness for the sake of the community.

## What is ScriptableObject Architecture?
The so-called ScriptableObject Architecture started spreading from some cursed Sessions of [2016 Unite](https://www.youtube.com/watch?v=6vmRwLYWNRo) and [2017 Unite](https://www.youtube.com/watch?v=raQ3iHhE_Kk). Now Unity sadly has a dedicated page on [How To](https://unity.com/how-to/architect-game-code-scriptable-objects) about this. But using ScriptableObject this way will bring your doom. Let's get to the reasons for not using it.

## Reason 1. They are meant to be used as Data Asset
ScriptableObject is meant to be used as immutable data asset. It's not Unreal Blueprint. Many Unity docs say it's good as data asset and data asset only. If someone is trying to set a dynamic string to TextAsset in runtime, that would seem nuts. Same applies to setting mutable values into ScriptableObject in runtime!

## Reason 2. You can do it with any C# Object
You know we can do it all that without SO and simpler. There is no single thing ScriptableObject can do but C# object can't. In contrast, there are tons of things that ScriptableObject can't, because of restriction and its nature. All the patterns, Observer, Strategy, Factory, Command, they can all be done by simple C# objects. You don't need to choose an unnecessarily complex way.

## Reason 3. Don't bind yourself to the Unity Inspector
Using ScriptableObject forces you and your team to be bound to Unity's GUI. Does it look cool to set a variable through the Editor? Okay to see through tutorials. Not until you have to search and roam to find the correct variable. Coupling your code with assets will make problems that are hard to find. Even worse is that it is not anywhere near flexible. Just using a proper Visual Scripting tool will be ten times more productive.

## Reason 4. It makes your project Unmaintainable
You cannot even tell what the problem is by looking at your code. You gotta debug your project with GUI. You have to make each the variable to link as an asset, per stat, per character. What are you going to do when you have to refactor your data structure? You cannot possibly imagine managing tons of ScriptableObject within a maze of directories. Is that really what you want?

## Reason 5. It lacks of Expandability
You can make a few variables that you can manage, but as the project expands, you will need lots of variables. Many of them have to be created at runtime. Since you cannot statically set it up as an asset, the whole purpose of SO architecture will be ruined. And you will realize it was dumb decision by the time you have to "Instantiate" ScriptableObject. It will be a long, painful journey to go back.

## Reason 6. There is ton of better Alternatives
What do you need? Do you need a reactive system? There is [UniRx](https://github.com/neuecc/UniRx), [UniTask](https://github.com/Cysharp/UniTask). Do you need Dependency Injection? There is [Zenject](https://github.com/modesttree/Zenject). Do you want to Visual Script? Use [Bolt](https://assetstore.unity.com/packages/tools/visual-scripting/bolt-163802)!

## Reason 7. You cannot turn off Domain/Scene Reload
According to [Unity's Document](https://docs.unity3d.com/Manual/SceneReloading.html), when you turn off Domain and Scene reloading for better performance of Play Mode, your Scriptable Object will **keep the value**. That's the price of messing up assets with mutable values. Who on earth will know what will happen when your core logic does not reset its value? You may never be able to turn them off.

## Conclusion
❌ **DO NOT USE ScriptableObject Architecture** ❌

Only use ScriptableObject when you need immutable data asset. If possible, don't use it at all. Editing design data with Unity Inspector is horrible. Use better alternative for this too, such as using [Spread Sheet](https://github.com/cathei/BakingSheet).
