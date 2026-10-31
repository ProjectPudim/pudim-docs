---
cover: ../../../assets/pudim-banner.png
coverY: 0
---

# Privacy Policy

**Last updated:** October 31, 2026

This policy explains what data **Pudim** collects, what it uses it for, where it is stored, for how long, and how you can request removal. It applies together with the [Terms of Service](service.md).

On Fluxer, bots receive the content of messages in the channels they can see. That is why we want to be clear about what Pudim does with it.

## Summary

- Pudim **reads messages** only to detect commands and mentions of the bot. **It does not store message content** in any database.
- Pudim only stores **server settings, warnings and reaction role menus**, plus the IDs needed for those features.
- Pudim **does not send DMs**, **does not use voice** and **does not record audio**.
- Pudim **does not sell** data and **does not use it for ads or profiling**.
- You can request removal of your data at any time (see section 10).

## 1. What data Pudim stores

### 1.1 Database (MongoDB)

| What is stored | Data | Purpose | Retention |
| --- | --- | --- | --- |
| **Server settings** | Server ID, prefix, auto role settings (role ID and whether it is enabled), automatic warning action rules (amount, action type, duration, channel ID) and the warning log channel ID | Making the bot work the way the server configured it | While the server uses the bot, or until a removal request |
| **Warnings** | Server ID, warned member ID, moderator ID, **reason written by the moderator**, warning ID and date | Moderation history (`warn`, `warnings`, `unwarn`, `clearwarns`) and automatic actions | Until a moderator removes the warning (`unwarn` or `clearwarns`), or until a removal request |
| **Reaction role menus** | Message ID, channel ID, server ID, ID of whoever created the menu, emojis used and which role each emoji grants | Granting roles when someone reacts | Until the menu is removed by the server, or until a removal request |
| **Language preference** | User ID and chosen language (default: Brazilian Portuguese) | Replying in the right language | Until a removal request |

### 1.2 Temporary cache (Valkey/Redis)

Pudim uses a cache to respond faster. It holds copies of data that already exists in the database, **for a short time**:

| Cached data | Duration |
| --- | --- |
| Server prefix | 1 hour |
| User language | 5 minutes |
| Interactive menu state | 10 minutes (temporary menus) or 1 hour (reaction role menus) |

The cache is also used to tell the bot that a server's prefix has changed.

### 1.3 Data the bot reads but does not store

To work, Pudim receives information from Fluxer, such as the ID and username of whoever runs a command, server, channel and role IDs, and a member's role list. This data is used **at the moment** of the command and is **not saved** in any database, except for what is described in section 1.1.

## 2. Message content

- Pudim reads incoming messages to know whether they start with a command prefix or mention the bot. After that, the message is **not saved**.
- Messages are **not stored** in any database or sent to external services.
- **Exception, the `purge` command:** when bulk-deleting messages, Pudim reads the selected messages and builds a plain-text backup file (date, username, content and attachment links). That file is **sent in the same channel** where the command was used, for the moderation team. **Pudim does not keep a copy of that file.** From then on, the file is under the server's control, and anyone with access to the channel may see it.
- **`massrole` command:** to apply a role to many members, Pudim temporarily fetches the server's member list (up to 1000). The list is used only while the command runs. **It is not saved, exported or shared.**

## 3. Server join and leave log

When Pudim joins or leaves a server, it sends a notice to a **private developer log channel** containing:

- the server name and ID;
- the member count;
- the server creation date;
- the server owner's username and ID;
- the server icon.

This is used to track the bot's growth and investigate problems. The notice goes to the Pudim team, **not** to your server.

## 4. External services

Pudim connects to the services below. **None of them receives messages, user IDs or server data.**

| Service | Purpose | What is sent |
| --- | --- | --- |
| **Fluxer** (API and gateway) | Running the bot on the platform | What is needed to run commands (see section 1.3) |
| **nekos.best** (`nekos.best/api/v2`) | Fetching animated images for interaction commands (`hug`, `pat`, `slap`, etc.) | Only the action name. As with any internet connection, the service can see the IP of the server hosting the bot |
| **Hosting (Discloud)** and **database and cache providers** | Keeping the bot online and storing the data in section 1 | The data in section 1, stored on their infrastructure |

If we start using another external service, this list will be updated.

## 5. Voice

Pudim **has no voice features**. It does not join voice channels and **does not record or transmit audio**. The `lock` and `unlock` commands only change voice channel permissions, such as speaking, and do not access audio.

## 6. Private messages and contacting you

Pudim **does not send DMs** and does not contact users on its own. It only replies in channels, in response to commands and interactions.

## 7. What we do not do

- We do not sell, rent or share data with advertisers.
- We do not build user profiles or track you across servers.
- We do not export member lists or scrape community data.
- We do not collect sensitive data on purpose. However, the **reason for a warning** is free text written by moderators. Please ask your server's moderators not to put sensitive personal data in it.

## 8. Sharing

Your data only leaves Pudim in the following situations:

- to the infrastructure providers in section 4, which store the data on our behalf;
- when required by law or by a competent authority;
- to protect the security of the bot, users or servers against abuse.

Inside a server, warnings and moderation logs may be seen by anyone with access to that server's moderation channels and commands.

## 9. Security

We use reasonable measures to protect data: the bot token and database credentials are kept in environment variables rather than in the code, and access to the infrastructure is restricted. No system is 100% secure, so we cannot guarantee absolute protection.

## 10. Your rights and how to remove your data

You may request:

- **access** to the data we hold about you;
- **correction** of incorrect data;
- **deletion** of data, such as warnings you received, your language preference or menus you created;
- clarification about how we handle your data.

**Server owners** may also request deletion of all of the server's settings.

To make a request, join the [support server](https://fluxer.gg/Ka4CXOqj) and talk to the team. To help us find your data, provide your user ID or the server ID.

**Warnings:** they exist for the server's moderation. If your server wants to remove a warning, its moderators can use `unwarn` or `clearwarns`. If you request deletion and there is a legitimate reason to keep a record (for example, security or compliance with a legal obligation), we will explain the reason.

We follow the rights set out in the Brazilian **General Data Protection Law (LGPD, Law 13,709/2018)**, where applicable.

## 11. Children and teenagers

Pudim is not directed at children. Using the bot depends on you being old enough to use Fluxer under the platform's rules. If we find data from someone who should not be using the service, we will remove it where possible.

## 12. Changes to this policy

We may update this policy. The "Last updated" date at the top shows the current version. Important changes, such as collecting new types of data, will be announced in the support server.

## 13. Contact

- **Support server:** <https://fluxer.gg/Ka4CXOqj>