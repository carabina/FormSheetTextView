### FormSheetTextView ![CocoaPods Version](https://img.shields.io/cocoapods/v/FormSheetTextView.svg?style=flat) ![Platform](https://img.shields.io/cocoapods/p/PageSheetForm.svg?style=flat) ![License](https://img.shields.io/cocoapods/l/PageSheetForm.svg?style=flat)

FormSheetTextView is a FormSheet style UITextView.

### Image
#### iPhone
<img src="https://user-images.githubusercontent.com/43707/29010740-6c126464-7b68-11e7-9a7d-a8a7d2e973e0.png" width="400px">

#### iPad
<img src="https://user-images.githubusercontent.com/43707/29011143-b37d892a-7b6b-11e7-9df5-28a0b8bdfc83.png" width="400px">

<img src="https://user-images.githubusercontent.com/43707/29011151-c7a805c4-7b6b-11e7-91e1-b15913d46938.png" width="400px">


### Examples

#### Swift

```html
import FormSheetTextView

        let formSheetTextViewController = FormSheetTextViewController.instantiate()
        formSheetTextViewController.setInitialText((self.baseTextView?.text)!)
        formSheetTextViewController.setTitleText("Title")
        formSheetTextViewController.setCancelButtonText("Cancel")
        
        // formSheetTextViewController.setTitleSize(20) // default 15
        // formSheetTextViewController.setButtonSize(20) // default 15

        formSheetTextViewController.setIsPreview(true)
        formSheetTextViewController.setPreviewPageTitle("Preview")
        formSheetTextViewController.setSendButtonText("Send")
        formSheetTextViewController.completionHandler = { sendText in
            
            if (sendText.characters.count > 20) {
                let alertController:UIAlertController = UIAlertController(title:nil, message: "The number of characters exceeds the upper limit. Please enter within 20 characters.", preferredStyle: UIAlertControllerStyle.alert)
                let cancelAction:UIAlertAction = UIAlertAction(title: "Close", style: UIAlertActionStyle.cancel, handler:{ (action:UIAlertAction!) -> Void in
                })
                alertController.addAction(cancelAction)
                formSheetTextViewController.present(alertController, animated: true, completion: nil)
                return
            }
            
            if (sendText.characters.count == 0) {
                let alertController:UIAlertController = UIAlertController(title:nil, message: "It is not input. Please enter.", preferredStyle: UIAlertControllerStyle.alert)
                let cancelAction:UIAlertAction = UIAlertAction(title: "Close", style: UIAlertActionStyle.cancel, handler:{ (action:UIAlertAction!) -> Void in
                })
                alertController.addAction(cancelAction)
                formSheetTextViewController.present(alertController, animated: true, completion: nil)
                return
            }
            
            
            // success
            self.baseTextView?.text = sendText
            
            self.dismiss(animated: true, completion: nil)
        };
        
        let navigationController = UINavigationController(rootViewController: formSheetTextViewController)
        navigationController.modalPresentationStyle = UIModalPresentationStyle.formSheet
        present(navigationController, animated: true, completion: nil)
```

#### ObjectiveC

```
@import FormSheetTextView;

__weak FormSheetTextViewController *formSheetTextViewController = [FormSheetTextViewController instantiate];
    [formSheetTextViewController setInitialText:@"initial text"];
    [formSheetTextViewController setTitleText:@"Title"];
    [formSheetTextViewController setCancelButtonText:@"Cancel"];
    [formSheetTextViewController setSendButtonText:@"Send"];
    [formSheetTextViewController setCompletionHandler:^(NSString *sendText) {
        
        if ([sendText length] > 5) {
            UIAlertController *alertController = [UIAlertController alertControllerWithTitle:nil message:@"The number of characters exceeds the upper limit. Please enter within 20 characters." preferredStyle:UIAlertControllerStyleAlert];
            UIAlertAction *cancelAction = [UIAlertAction actionWithTitle:@"Cancel" style:UIAlertActionStyleDefault handler:^(UIAlertAction *action) {}];
            [alertController addAction:cancelAction];
            [formSheetTextViewController presentViewController:alertController animated:YES completion:nil];

            return;
        }
        
        if ([sendText length] == 0) {
            UIAlertController *alertController = [UIAlertController alertControllerWithTitle:nil message:@"It is not input. Please enter.." preferredStyle:UIAlertControllerStyleAlert];
            UIAlertAction *cancelAction = [UIAlertAction actionWithTitle:@"Cancel" style:UIAlertActionStyleDefault handler:^(UIAlertAction *action) {}];
            [alertController addAction:cancelAction];
            [formSheetTextViewController presentViewController:alertController animated:YES completion:nil];
            
            return;
        }
        
        [self dismissViewControllerAnimated:true completion:nil];
    }];

    UINavigationController *navigationController = [[UINavigationController alloc] initWithRootViewController:formSheetTextViewController];
    [navigationController setModalPresentationStyle:UIModalPresentationFormSheet];
    [self presentViewController:navigationController animated:true completion:nil];
```

### Installation (CocoaPods)
`pod FormSheetTextView`
