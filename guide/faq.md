The following are a list of frequently asked questions.

## Why is the text empty when I select words in some applications?

Some applications on macOS do not support native Accessibility for word selection. For this situation, Easydict provides a forced word selection feature: simulate `⌘ + C` shortcut to copy text. You can enable this feature in `Settings -> General -> Force Selection`.

> Warning⚠️: This feature is experimental and enabling it may cause the `⌘ + C` copy function to behave abnormally in some applications.

## Why can't I use mouse hover to select words in some applications?

By default, only applications that support Accessibility can use mouse hover to select words. If you encounter an application that cannot use mouse hover to select words, please try to enable `Force Selection`.

If it still doesn't work, please refer to [Cannot use hover translation in specific applications](https://github.com/tisfeng/Easydict/issues/84) to submit an issue.

## Why is there a beep when the selected word is empty (such as dragging in a blank area) in some applications?

In applications that do not support native Accessibility for word selection, when using `⌘ + C` to force word selection, a system beep may be triggered. This is because some applications do not support empty copy operations.

Enabling the `Disable Beep for Empty Copy` option in the settings can avoid this problem to some extent.

## Why does the edit button in the upper right corner flicker when selecting words in some applications?

This is a known issue. When Accessibility word selection fails, it will try to simulate the `⌘ + C` shortcut to force word selection. This operation will trigger the [Edit - Copy] action, which will flash in some applications.

## Why might selecting an empty word interrupt the music currently playing?

This may be caused by enabling the `Disable Beep for Empty Copy` option. The implementation principle of this feature is that if it detects that the current device is not playing music, it will briefly mute the system volume.

However, in some scenarios, this detection judgment may not be accurate, so even if the user is playing music, it may still cause the music to be briefly muted.

We currently do not have a good solution to this problem. If you have one, please feel free to submit a PR.

## Why do word selection and OCR need to enable system-related permissions?

Due to the strict permission management of the macOS platform, some features must enable the corresponding permissions to be used normally. Specifically:

- Easydict needs to enable `Accessibility` permissions to get the text currently selected by the user;
- Easydict needs to enable `Screen Recording` permissions to use the screenshot translation feature.

Easydict is open source software. If you have any concerns about privacy, you can check the code.

> [!NOTE]
> The above two permissions will be automatically requested when Easydict first uses the corresponding features. If the authorization fails, you need to enable it yourself in the system settings later.

## Why can't I select words on some web pages in the browser?

The Easydict word selection process is: Accessibility > AppleScript > Simulate `⌘ + C` shortcut.

It prefers to use Accessibility for word selection. When Accessibility word selection fails (unauthorized or the application does not support), if it is a browser application (such as Safari, Chrome), it will try to use AppleScript for word selection. If AppleScript word selection still fails, it will finally force word selection—simulate `⌘ + C` shortcut for word selection.

Therefore, it is recommended to enable the `Allow JavaScript in Apple Events` option in the browser. This can avoid event interception on some web pages, such as [web pages forcibly attaching copyright information](https://github.com/tisfeng/Easydict/issues/85) issues, and optimize the word selection experience.

For Safari users, it is strongly recommended to enable this option, because Safari does not support Accessibility word selection, and AppleScript word selection experience is far superior to simulating shortcut word selection.

<table>
    <td> <img src="https://raw.githubusercontent.com/tisfeng/ImageBed/main/uPic/image-20230708115811617-1688788691.png"></td>
    <td> <img src="https://raw.githubusercontent.com/tisfeng/ImageBed/main/uPic/image-20230708115827839-1688788707.png"></td>
</table>

## Why does macOS still pop up asking for permissions even though I have given Easydict the Accessibility/Screen Recording permissions?

1. Please go to `Settings` -> `Privacy & Security` -> `Accessibility` -> click `-` to remove Easydict from the list and then re-add it.

<img width="751" alt="image" src="https://github.com/tisfeng/Easydict/assets/25194972/cd3961a9-8baf-42de-97fc-6acc3cb30b03">

2. If method 1 is invalid, you can try to use the command in the terminal to reset Easydict's permissions:

```shell
tccutil reset Accessibility com.izual.Easydict
```

Then restart the computer, restart Easydict authorization.

3. If method 2 is still ineffective, please try to use the following command to reset the auxiliary function permissions of all Apps:

```shell
tccutil reset Accessibility
```

Then restart the computer, restart Easydict authorization.

If all of the above methods do not work, please open an issue to feedback.
