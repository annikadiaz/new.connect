# My Portfolio

I am a recent graduate from The Ohio State University and am working to learn the basics of app development and design. 
The majority of my coding experience has been for the purpose of statistical analysis in biological research. 
I am looking forward to becoming more confident and comfortable with coding by learning Swift! 

## View My Most Recent Work

I am currently enrolled in a coding course to learn Swift and the basics of app development and design. 
Through the course I am able to work on guided projects to learn and apply different Swift concepts 

## Hangman Style Game 
Through the course our first larger project was a word guessing game similar to Hangman, but with a tree that would lose apples 
as the player selected incorrect letters. 
```
//
//  ViewController.swift
//  Apple Pie
//
//  Created by Annika Diaz on 5/27/21.
//

import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        newRound()
        // Do any additional setup after loading the view.
    }
    
    @IBOutlet var treeImageView: UIImageView!
    @IBOutlet var correctWordLabel: UILabel!
    @IBOutlet var scoreLabel: UILabel!
    @IBOutlet var letterButtons: [UIButton]!
    
    var listOfWords = ["plant", "house", "animal", "research", "disease", "doctor"]
    let incorrectMovesAllowed = 7
    var totalWins = 0 {
        didSet {
            newRound ()
        }}
    var totalLosses = 0{
        didSet {
            newRound()
        }}
    
    var currentGame: Game!
    
    func updateUI() {
        var letters = [String]()
        for letter in currentGame.formattedWord {
            letters.append(String(letter))
        }
        let wordWithSpacing = letters.joined(separator: " ")
        correctWordLabel.text = wordWithSpacing
        scoreLabel.text = "Wins: \(totalWins), Losses: \(totalLosses)"
        treeImageView.image = UIImage(named: "Tree \(currentGame.incorrectMovesRemaining)")
    }
    
    func updateGameState() {
        if currentGame.incorrectMovesRemaining == 0 {
            totalLosses += 1
        } else if currentGame.word == currentGame.formattedWord {
            totalWins += 1
        } else {
            updateUI()
        }
    }
    
    @IBAction func buttonPressed(_ sender: UIButton) {
        sender.isEnabled = false
        let letterString = sender.title(for: .normal)!
        let letter = Character(letterString.lowercased())
        currentGame.playerGuessed(letter: letter)
        updateGameState()
    }

    func enableLetterButtons(_ enable: Bool) {
        for button in letterButtons {
            button.isEnabled = enable
        }
    }
    
    func newRound() {
        if !listOfWords.isEmpty {
        let newWord = listOfWords.removeFirst()
        currentGame = Game(word: newWord, incorrectMovesRemaining: incorrectMovesAllowed, guessedLetters:[])
        enableLetterButtons(true)
        updateUI()
        } else {
            enableLetterButtons(false)
        }}
}//Annika Diaz 5/28/21
```

![Screen Shot 2021-05-30 at 1 27 35 PM](https://user-images.githubusercontent.com/84987285/120113941-cf9f5b00-c14a-11eb-8de8-3cf8da952727.png)



