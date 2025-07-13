using System;
using System.Collections.Generic;
using System.Linq;

public class CalculatorApp
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Console Calculator – Phase 3");
        Console.WriteLine("Prepared by: Morgan Moore\n");

        MemoryManager memory = new MemoryManager();

        bool running = true;
        while (running)
        {
            DisplayMenu();
            Console.Write("Enter your choice: ");
            string choice = Console.ReadLine();

            switch (choice)
            {
                case "1":
                    Console.Write("Enter a value to store in memory: ");
                    if (double.TryParse(Console.ReadLine(), out double val))
                        memory.StoreSingle(val);
                    break;
                case "2":
                    memory.RetrieveSingle();
                    break;
                case "3":
                    memory.ClearSingle();
                    break;
                case "4":
                    Console.Write("Enter new value to replace memory: ");
                    if (double.TryParse(Console.ReadLine(), out double newVal))
                        memory.ReplaceSingle(newVal);
                    break;
                case "5":
                    Console.Write("Enter integer value to add to collection: ");
                    if (int.TryParse(Console.ReadLine(), out int newInt))
                        memory.AddToCollection(newInt);
                    break;
                case "6":
                    memory.DisplayCollection();
                    break;
                case "7":
                    Console.Write("Enter value to remove from collection: ");
                    if (int.TryParse(Console.ReadLine(), out int removeVal))
                        memory.RemoveFromCollection(removeVal);
                    break;
                case "8":
                    memory.DisplayCount();
                    break;
                case "9":
                    memory.SumCollection();
                    break;
                case "10":
                    memory.AverageCollection();
                    break;
                case "11":
                    memory.DifferenceFirstLast();
                    break;
                case "0":
                    running = false;
                    Console.WriteLine("Thank you for using the calculator. Goodbye!");
                    break;
                default:
                    Console.WriteLine("Invalid option. Please try again.\n");
                    break;
            }
        }
    }

    public static void DisplayMenu()
    {
        Console.WriteLine("\nMemory Function Menu:");
        Console.WriteLine("1. Store single value");
        Console.WriteLine("2. Retrieve single value");
        Console.WriteLine("3. Clear single value");
        Console.WriteLine("4. Replace single value");
        Console.WriteLine("5. Add value to memory collection");
        Console.WriteLine("6. Display all values in memory collection");
        Console.WriteLine("7. Remove value from collection");
        Console.WriteLine("8. Display count of values");
        Console.WriteLine("9. Sum of values");
        Console.WriteLine("10. Average of values");
        Console.WriteLine("11. Difference of first and last values");
        Console.WriteLine("0. Quit");
    }
}

public class MemoryManager
{
    private double? singleValue = null;
    private List<int> memoryCollection = new List<int>();
    private const int MaxSize = 10;

    public void StoreSingle(double value)
    {
        singleValue = value;
        Console.WriteLine($"Stored {value} in single memory.\n");
    }

    public void RetrieveSingle()
    {
        if (singleValue.HasValue)
            Console.WriteLine($"Single memory contains: {singleValue.Value}\n");
        else
            Console.WriteLine("No value stored in single memory.\n");
    }

    public void ClearSingle()
    {
        singleValue = null;
        Console.WriteLine("Single memory cleared.\n");
    }

    public void ReplaceSingle(double value)
    {
        singleValue = value;
        Console.WriteLine($"Single memory replaced with: {value}\n");
    }

    public void AddToCollection(int value)
    {
        if (memoryCollection.Count < MaxSize)
        {
            memoryCollection.Add(value);
            Console.WriteLine($"Added {value} to memory collection.\n");
        }
        else
        {
            Console.WriteLine("Memory collection is full (10 values max).\n");
        }
    }

    public void DisplayCollection()
    {
        if (memoryCollection.Count == 0)
        {
            Console.WriteLine("Memory collection is empty.\n");
            return;
        }
        Console.WriteLine("Memory collection values:");
        foreach (var val in memoryCollection)
            Console.Write(val + " ");
        Console.WriteLine("\n");
    }

    public void RemoveFromCollection(int value)
    {
        if (memoryCollection.Remove(value))
            Console.WriteLine($"Removed {value} from collection.\n");
        else
            Console.WriteLine($"Value {value} not found in collection.\n");
    }

    public void DisplayCount()
    {
        Console.WriteLine($"There are {memoryCollection.Count} value(s) stored in the collection.\n");
    }

    public void SumCollection()
    {
        int sum = memoryCollection.Sum();
        Console.WriteLine($"Sum of values in collection: {sum}\n");
    }

    public void AverageCollection()
    {
        if (memoryCollection.Count == 0)
        {
            Console.WriteLine("Cannot compute average – collection is empty.\n");
            return;
        }
        double average = memoryCollection.Average();
        Console.WriteLine($"Average of values: {average:F2}\n");
    }

    public void DifferenceFirstLast()
    {
        if (memoryCollection.Count < 2)
        {
            Console.WriteLine("Need at least two values to compute difference.\n");
            return;
        }
        int diff = memoryCollection.First() - memoryCollection.Last();
        Console.WriteLine($"Difference between first and last: {diff}\n");
    }
}
```
