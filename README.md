import java.util.Random;

class Player {
    private String name;
    private int health;
    private int strength;
    private int attack;

    public Player(String name, int health, int strength, int attack) {
        this.name = name;
        this.health = health;
        this.strength = strength;
        this.attack = attack;
    }

    public void attack(Player opponent) {
        Random rand = new Random();
        int attackingDieRoll = rand.nextInt(6) + 1;
        int defendingDieRoll = rand.nextInt(6) + 1;

        int attackDamage = attackingDieRoll * attack;
        int defendStrength = defendingDieRoll * opponent.strength;

        int damageTaken = Math.max(0, attackDamage - defendStrength);
        opponent.health -= damageTaken;

        System.out.println(name + " attacks " + opponent.name + ":");
        System.out.println("Attacking die roll: " + attackingDieRoll);
        System.out.println("Defending die roll: " + defendingDieRoll);
        System.out.println("Attack damage: " + attackDamage);
        System.out.println(opponent.name + "'s health reduced by " + damageTaken + " to " + opponent.health);
        System.out.println();
    }

    public boolean isAlive() {
        return health > 0;
    }
}

public class MagicalArena {
    public static void main(String[] args) {
        Player playerA = new Player("Player A", 50, 5, 10);
        Player playerB = new Player("Player B", 100, 10, 5);

        while (playerA.isAlive() && playerB.isAlive()) {
            playerA.attack(playerB);
            if (!playerB.isAlive()) {
                System.out.println("Player A wins!");
                break;
            }

            playerB.attack(playerA);
            if (!playerA.isAlive()) {
                System.out.println("Player B wins!");
                break;
            }
        }

        if (playerA.isAlive() && playerB.isAlive()) {
            System.out.println("It's a draw!");
        }
    }
}
