# DGD203-hibamerimi
﻿using System;

namespace CarGame
{
    // The Car class
    public class Car
    {
        // Properties
        public string Model { get; private set; }
        public float Speed { get; private set; } // Current speed in km/h
        public float MaxSpeed { get; private set; } // Maximum speed the car can achieve
        public float Fuel { get; private set; } // Current fuel level in liters
        public float FuelCapacity { get; private set; } // Maximum fuel capacity
        public float Health { get; private set; } // Health of the car
        public float MaxHealth { get; private set; } // Maximum health

        // Constructor
        public Car(string model, float maxSpeed, float fuelCapacity, float maxHealth)
        {
            Model = model;
            MaxSpeed = maxSpeed;
            FuelCapacity = fuelCapacity;
            Fuel = fuelCapacity; // Start with a full tank
            MaxHealth = maxHealth;
            Health = maxHealth; // Start with full health
        }

        // Methods
        public void Accelerate(float amount)
        {
            if (Fuel <= 0)
            {
                Console.WriteLine($"{Model} has no fuel to accelerate!");
                return;
            }

            Speed += amount;
            if (Speed > MaxSpeed)
            {
                Speed = MaxSpeed;
            }
            Fuel -= amount * 0.05f; // Consumes fuel as it accelerates

            if (Fuel < 0) Fuel = 0;
            Console.WriteLine($"{Model} accelerates to {Speed} km/h. Fuel remaining: {Fuel:F2}L.");
        }

        public void Brake(float amount)
        {
            Speed -= amount;
            if (Speed < 0) Speed = 0;
            Console.WriteLine($"{Model} slows down to {Speed} km/h.");
        }

        public void Refuel(float amount)
        {
            Fuel += amount;
            if (Fuel > FuelCapacity)
            {
                Fuel = FuelCapacity;
            }
            Console.WriteLine($"{Model} refueled to {Fuel:F2}L.");
        }

        public void TakeDamage(float damage)
        {
            Health -= damage;
            if (Health < 0) Health = 0;
            Console.WriteLine($"{Model} takes {damage} damage. Health remaining: {Health}/{MaxHealth}.");
        }

        public void Repair(float amount)
        {
            Health += amount;
            if (Health > MaxHealth)
            {
                Health = MaxHealth;
            }
            Console.WriteLine($"{Model} repaired to {Health}/{MaxHealth}.");
        }

        public void Status()
        {
            Console.WriteLine($"Car: {Model}");
            Console.WriteLine($"Speed: {Speed} km/h");
            Console.WriteLine($"Fuel: {Fuel}/{FuelCapacity}L");
            Console.WriteLine($"Health: {Health}/{MaxHealth}");
        }
    }

    // Main program
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new car
            Car playerCar = new Car("Speedster GT", 200, 50, 100);

            // Simulate game interactions
            playerCar.Status();
            playerCar.Accelerate(30); // Accelerates
            playerCar.TakeDamage(20); // Takes some damage
            playerCar.Brake(10); // Slows down
            playerCar.Refuel(20); // Refuels
            playerCar.Repair(15); // Repairs some health
            playerCar.Accelerate(50); // Accelerates again
            playerCar.Status(); // Check the final status
        }
    }
}
