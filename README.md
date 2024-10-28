using System;
using System.Collections.Generic;

namespace PollutionTracker
{
    class Program
    {
        public class PollutionRecord
        {
            public string Location { get; set; }
            public DateTime Date { get; set; }
            public double PollutionLevel { get; set; }

            public PollutionRecord(string location, DateTime date, double pollutionLevel)
            {
                Location = location;
                Date = date;
                PollutionLevel = pollutionLevel;
            }

            public override string ToString()
            {
                return $"{Date.ToShortDateString()} - {Location}: {PollutionLevel} µg/m³";
            }
        }

        static List<PollutionRecord> records = new List<PollutionRecord>();

        static void Main(string[] args)
        {
            string command;

            do
            {
                Console.WriteLine("Введите команду: add, list, average, exit");
                command = Console.ReadLine();

                switch (command)
                {
                    case "add":
                        AddRecord();
                        break;
                    case "list":
                        ListRecords();
                        break;
                    case "average":
                        CalculateAverage();
                        break;
                }
            } while (command != "exit");
        }

        static void AddRecord()
        {
            Console.Write("Введите местоположение: ");
            string location = Console.ReadLine();

            Console.Write("Введите дату (yyyy-mm-dd): ");
            DateTime date = DateTime.Parse(Console.ReadLine());

            Console.Write("Введите уровень загрязнения (µg/m³): ");
            double level = Convert.ToDouble(Console.ReadLine());

            records.Add(new PollutionRecord(location, date, level));
            Console.WriteLine("Запись добавлена.");
        }

        static void ListRecords()
        {
            Console.WriteLine("Записи о загрязнении:");
            foreach (var record in records)
            {
                Console.WriteLine(record);
            }
        }

        static void CalculateAverage()
        {
            if (records.Count == 0)
            {
                Console.WriteLine("Нет записей для расчета.");
                return;
            }

            double total = 0;
            foreach (var record in records)
            {
                total += record.PollutionLevel;
            }

            double average = total / records.Count;
            Console.WriteLine($"Средний уровень загрязнения: {average} µg/m³");
        }
    }
}
