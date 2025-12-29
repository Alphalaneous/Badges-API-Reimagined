# Badges API Reimagined

An API for adding badges to profiles and comments easily.

## The API

It is extremely simple, here's an example on how to register and modify badge:

```cpp
$execute {
    BadgesAPI::registerBadge(
        // A unique ID for your badge.
        "your-badge-id"_spr, 
        // The name shown when clicking the badge.
        "Badge Name", 
        // The description shown when clicking the badge.
        "This is a description that goes along with the badge.", 
        // Create a node that you want to use as the badge, it will be sized accordingly automatically.
        [] {
            return CCSprite::createWithSpriteFrameName("modBadge_01_001.png");
        },
        // Show the badge when a profile/comment is loaded.
        // BadgesAPI::showBadge can be called at any time and simply requires the Badge object.
        // UserInfo contains the username, account ID, user ID, and moderator information.
        [] (const Badge& badge, const UserInfo& info) {
            if (info.modStatus == ModStatus::REGULAR) BadgesAPI::showBadge(badge);
        }
    );

    // Unregistering.
    BadgesAPI::unregisterBadge("your-badge-id"_spr);

    // Setting name.
    BadgesAPI::setName("your-badge-id"_spr, "New Badge Name");

    // Setting description.
    BadgesAPI::setDescription("your-badge-id"_spr, "New Description");

    // Setting the callback for creating the badge node.
    BadgesAPI::setCreateBadgeCallback("your-badge-id"_spr, [] {
        return CCSprite::createWithSpriteFrameName("modBadge_02_001.png");
    });

    // Setting the callback for showing the badge when a profile/comment is loaded.
    BadgesAPI::setProfileCallback("your-badge-id"_spr, [] (const Badge& badge, const UserInfo& info) {
        if (info.userName == "Alphalaneous") BadgesAPI::showBadge(badge);
    });

    // Getting the name.
    log::info("Name: {}", BadgesAPI::getName("your-badge-id"_spr));

    // Getting the description.
    log::info("Description: {}", BadgesAPI::getDescription("your-badge-id"_spr));
}
```

**Mod badge descriptions from https://www.robtopgames.com/faq/en/answers/moderator/**