# iOSPT Demo Day

## Requirements

1. Fork and clone the repository
2. **Add your presentation content**
    1. Slide deck (4 required slides)
    2. Links
    3. Answer all questions 
    4. YouTube demo video (1-2 min max)
3. Polish your Github Code repository
    1. Add screenshots and an overview to your GitHub Code Repository
    2. You should make that repository the "Public Portfolio" for your project
    3. Look at [John Sundell's Splash project](https://github.com/JohnSundell/Splash) for inspiration (code, images, GIFs)
4. Create a pull request (PR) and **tag your TL and Instructor**

## Links

* Github Code: https://github.com/iOSPT5-BW1/Ad-Libs/pull/7
* Github Proposal: https://github.com/LambdaSchool/ios-build-sprint-project-proposal/pull/70
* Trello/Github Project Kanban: https://www.notion.so/5ed6f4c98b33493b92368d2a17452a00?v=cd332a0244a246e3a998f4cd3c9b0e7d
* Test Flight Signup (Recommended): `<insert beta signup link here>`
* YouTube demo video (Recommended): https://youtu.be/S2UgdrnNV-4

## Hero Image

`<Post one screenshot in an iPhone Simulator frame or an iPhone 11 Pro render using placeit.com>`

## Questions (Answer indented below)

1. What was your favorite feature to implement? Why?

    `<Your answer here>`

2. What was your #1 obstacle or bug that you fixed? How did you fix it?

    `Switching between a new adlib and an existing one pulled from the tableView.  this was fixed by implementng a .state check for which the user was coming from.
  
3. Share a chunk of code (or file) you're proud of and explain why.

The theme settings file from the app, where the user can select a color from a picker and it auto-updates when landing on the selection, as well as the persistent selection of which story (only during the running of the app)the user chose to run with:
(I would like to make this more elegant and move the selection process to a helper file but am struggling with the 'view.backgroundColor' mode from within a non-Cocoa Touch Class file as of yet.

    import UIKit

protocol ThemeSelectedDelegate {
    func themeChosen()
}
class SettingsViewController: UIViewController, UIPickerViewDelegate, UIPickerViewDataSource {
    var pickerData = ["Blue", "Cyan", "Dark", "Gray", "Green","Light", "Orange", "Purple", "Teal", "Yellow"]
    
    @IBOutlet weak var themePicker: UIPickerView!
    @IBOutlet weak var story1Button: UIButton!
    @IBOutlet weak var story2Button: UIButton!
    @IBOutlet weak var story3Button: UIButton!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        themePicker.delegate = self
        themePicker.selectRow(Settings.shared.changeBackground, inComponent:
            0, animated: true)
        themePicker.backgroundColor = UIColor(white: 1, alpha: 0.35)
        themePicker.layer.borderColor = UIColor.white.cgColor
        themePicker.layer.borderWidth = 2.5
        themePicker.layer.cornerRadius = 7.5
        customizeButtons(sender: 0)
        
        updateViews()
    }
    
    func customizeButtons(sender: Int) {
          Settings.shared.storyChanged = true
        switch sender {
        case 0:
            story1Button.layer.borderColor = UIColor.red.cgColor
            story1Button.layer.borderWidth = 2.5
            story1Button.layer.cornerRadius = 8.0
            story1Button.backgroundColor = UIColor.init(red: 255/255, green: 0/255, blue: 0/255, alpha: 0.55)
            story2Button.layer.borderColor = UIColor.clear.cgColor
            story3Button.layer.borderColor = UIColor.clear.cgColor
            story2Button.backgroundColor = .clear
            story3Button.backgroundColor = .clear
            Settings.shared.story = .story1
        case 1:
            story2Button.layer.borderColor = UIColor.red.cgColor
            story2Button.layer.borderWidth = 2.5
            story2Button.layer.cornerRadius = 8.0
            story2Button.backgroundColor = UIColor.init(red: 255/255, green: 0/255, blue: 0/255, alpha: 0.55)
            story1Button.layer.borderColor = UIColor.clear.cgColor
            story3Button.layer.borderColor = UIColor.clear.cgColor
            story1Button.backgroundColor = .clear
            story3Button.backgroundColor = .clear
            Settings.shared.story = .story2
        case 2:
            story3Button.layer.borderColor = UIColor.red.cgColor
            story3Button.layer.borderWidth = 2.5
            story3Button.layer.cornerRadius = 8.0
            story3Button.backgroundColor = UIColor.init(red: 255/255, green: 0/255, blue: 0/255, alpha: 0.55)
            story1Button.layer.borderColor = UIColor.clear.cgColor
            story2Button.layer.borderColor = UIColor.clear.cgColor
            story1Button.backgroundColor = .clear
            story2Button.backgroundColor = .clear
            Settings.shared.story = .story3

        default:
            break
        }
    }
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(true)
        setTheme()
    }
    
    func numberOfComponents(in pickerView: UIPickerView) -> Int {
        1
    }
    
    func pickerView(_ pickerView: UIPickerView, numberOfRowsInComponent component: Int) -> Int {
        pickerData.count
    }
    
    func pickerView(_ pickerView: UIPickerView, titleForRow row: Int, forComponent component: Int) -> String? {
        return pickerData[row]
    }
    
    func pickerView(_ pickerView: UIPickerView, didSelectRow row: Int, inComponent component: Int) {
        Settings.shared.changeBackground = themePicker.selectedRow(inComponent: 0)
        UserDefaults.standard.set(Settings.shared.changeBackground, forKey: "themeSet")
        setTheme()
    }
    
    func setTheme() {
        switch Settings.shared.changeBackground {
        case 0:
            view.backgroundColor = .blue
        case 1:
            view.backgroundColor = UIColor(red: 129/255, green: 194/255, blue: 183/255, alpha: 1.0)
        case 2:
            view.backgroundColor = .darkGray
        case 3:
            view.backgroundColor = .systemGray3
        case 4:
            view.backgroundColor = .systemGreen
        case 5:
            view.backgroundColor = .lightGray
        case 6:
            view.backgroundColor = .systemOrange
        case 7:
            view.backgroundColor = .systemPurple
        case 8:
            view.backgroundColor = .systemTeal
        case 9:
            view.backgroundColor = .yellow
        default:
            break
        }
    }
    
    func updateViews() {
        setTheme()
    }
    
    @IBAction func storySelectButtonPressed(_ sender: UIButton) {
      
        if Settings.shared.storyChanged {
        customizeButtons(sender: sender.tag)
        } else if !Settings.shared.storyChanged {
            customizeButtons(sender: 0)
        }
    }
}

  
4. What is your elevator pitch? (30 second description your Grandma or a 5-year old would understand)

    Want to have fun when bored? PLay this ad-lib game that makes funny sentences from words you give or random ones, with cool colors to boot!
  
5. What is your #1 feature?

    The randomizer within that randomly picks an ad-lib story with randomly generated words that fill in.
  
6. What are you future goals?

    We would like to have more stories to choose from, grow the words picked from from words entered by the user, and graphics where, utilizing SpriteKit maybe, that the words POOF into each spot!

## Required Slides (Add your Keynote to your PR)

1. App Name / Team Slide
2. Elevator Pitch
3. Your #1 Feature (Customer facing — what can I do with your app?)
4. Future Goals

## Slide Requirements

1. 50 pt font minimum
2. Be concise — don't write sentences/paragraphs (put these in your slide notes for speaking)
3. 3-6 bullets maximum per slide
4. Do the squint test (can you read the text if you squint, if so, make the font bigger)
6. Images are always welcome
7. Do the Grandma Test (Would your Grandma understand you?)

### Optional Slides

1. Blooper: What's a funny bug or blooper? (screenshots/GIFs please)
2. Revenue Model: If the app was your sole source of income, how would you monetize it?

## Presentation Format

**7 minutes/team**

* 4 minute presentation (5 minute hard cap)
* 3 minutes of questions

We have ~12 teams presenting today — please practice your presentation with a timer (as a team), and make sure you fit within the time limit.

Plan on having one person present the slides and live demo. Please practice your presentation in front of a mirror or with your team 2-5 times. Have the app running and visible (Simulator or QuickTime) so you can quickly transition between slides and live demo.

* App Name / Team Slide (30 seconds)
* Elevator Pitch Slide (30 seconds)
* Your #1 Feature (30 seconds)
* Live Demo (2 minutes)
* Future Goals (30 seconds)
* Questions (3 minutes)
