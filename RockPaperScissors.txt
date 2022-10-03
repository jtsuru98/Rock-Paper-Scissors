import java.util.*;

public class RockPaperScissors
{
    public static void rulesOfTheGame(){
        System.out.println("Here are the rules of the game: ");
        System.out.println("-Best two out of three. Against the computer.");
        System.out.println("-You can choose between rock, paper, and scissor.");
        System.out.println("   -Rock beats scissor and loses to paper.");
        System.out.println("   -Paper beats rock and loses to scissor.");
        System.out.println("   -Scissor beats paper and loses to rock.");
        System.out.println("-Make sure your spelling is accurate (rock, paper, scissor). You get three attempts throughout the game.\n");
    }
    public static void playGame(String player) {
        rulesOfTheGame();
        
        String[] computerOptions = {"rock", "paper", "scissor"}; // used to randomly determine computer move
        List<String> allMoves = new ArrayList<>(Arrays.asList(computerOptions)); //used for input validation (i.e. user chooses rock, paper, or scissor)
        
        System.out.println("Let's get started....");
        System.out.println("When I say 'rock, paper, scissor, shoot!,' pick your weapon.");
        System.out.println("If you need a refresher, type 'rules please'\n");
        
        int userScore = 0;
        int computerScore = 0;
        int userErrorInput = 0;
		
		Scanner userInput = new Scanner(System.in);
		Random computerInput = new Random(); 
		
        while (userScore < 2 && computerScore < 2 && userErrorInput < 3) {
            System.out.println("rock, paper, scissor, shoot!");
            
            String userMove = userInput.nextLine().toLowerCase(); // user input
            String computerMove = computerOptions[computerInput.nextInt(computerOptions.length)]; // computer input
            
            //1) if user requests rules, print out rules 
            if (userMove.equals("rules please")){
                System.out.println();
                rulesOfTheGame();
                System.out.println("now...where were we?");
            }
            //2) if user input not in computer options, give a warning. once it hits 3, disaqualify player
            else if (allMoves.contains(userMove) == false){
                userErrorInput += 1;
                System.out.println("Strike " + userErrorInput + "! If you hit three strikes, you automatically lose.");
            }
            //3) if user "beats" computer, tally and say they won
            else if ((userMove.equals("rock") && computerMove.equals("scissor")) || (userMove.equals("paper") && computerMove.equals("rock")) 
            || (userMove.equals("scissor") && computerMove.equals("paper"))) {
                userScore += 1;
                System.out.println("You won! Score is now " + player + ": " + userScore + " Computer: " + computerScore);
            }
            //4) if tie, say they tied
            else if (userMove.equals(computerMove)) {
                System.out.println("You tied! Play again. Score remains " + player + ": " + userScore + " Computer: " + computerScore);
            }
            //5) else, computer wins and say they lost
            else {
                computerScore += 1;
                System.out.println("You lost! Score is now " + player + ": " + userScore + " Computer: " + computerScore);
            }
        }
        // once the game is done, print out the result
        if (userScore > computerScore) {
            System.out.println("\nCongratulations " + player + "!. You won by a score of " + userScore + " to " + computerScore + ".");
        }
        else if (userScore < computerScore){
            System.out.println("\nSorry " + player + "!. You lost by a score of " + computerScore + " to " + userScore + ".");
        }
        else {
            System.out.println("\nYou are disqualified! Try spelling your words right next time!");
        }
    }
    
    public static void main(String[] args) {
        System.out.println("Welcome to Rock, Paper, Scissors."); 
        System.out.println("Enter your name player.");
        
        Scanner player = new Scanner(System.in);
        String newPlayer = player.nextLine();
        if (newPlayer.length() == 0){
            System.out.println("That is not a valid name. Please try again.");
            System.exit(0);
        }

        System.out.println("Thank you " + newPlayer + ". Now let's start with the rules...\n");
        playGame(newPlayer);
    }
}