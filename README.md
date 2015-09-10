program
----
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using SharesBusiness;

namespace SharesAccountingSystem
{
    class Program
    {
        static void Main(string[] args)
        {
            int commandNumber;
            MemberUI memberUI = new MemberUI();

            WriteApplicationBanner();
            commandNumber = WriteCommands();

            do
            {
                if (commandNumber==4)
                {
                    break;
                }

                switch (commandNumber)
                {
                    case 1:
                        memberUI.AddNew();
                        break;
                    case 3:
                        memberUI.GetAll();
                        break;
                    default:
                        Console.WriteLine("Invalid Command...!!!");
                        break;
                }

                commandNumber = WriteCommands();

            } while (commandNumber != 4);

            Console.WriteLine("=============================================================================\n");
            Console.WriteLine("  ************** Thank You **************\n");
            Console.WriteLine("=============================================================================\n");

            Console.ReadKey();
        }

        static void WriteApplicationBanner()
        {
            Console.WriteLine("=============================================================================\n");
            Console.WriteLine("  ************** Welcome to New Paramatrix Co-operative Bank **************\n");
            Console.WriteLine("=============================================================================\n");
        }

        static int WriteCommands()
        {
            int commandNumber;

            Console.WriteLine("1. Add New Customer\n");
            Console.WriteLine("2. Delete Customer\n");
            Console.WriteLine("3. View All Customers\n");
            Console.WriteLine("4. Exit the Program\n");
            Console.Write("Select Command (enter command number): ");
            commandNumber = Convert.ToInt32(Console.ReadLine());
            Console.WriteLine("=============================================================================\n");

            return commandNumber;
        }
    }
}

// member form-----
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using SharesBusiness;

namespace SharesAccountingSystem
{
    internal class MemberUI
    {
        public void AddNew()
        {
            try
            {
                Member newMember = new Member(@"D:\ParaCustomer.txt");

                //Member newMember1 = new Member(MemberTitle.Mr, "Ajay", "Sharma", MemberType.Nominal, @"D:\ParaCustomer.txt");

                char addConfirmation = 'N';
                char newEntryConfirmation = 'N';

                do
                {
                    Console.Write("Member Title: ");
                    newMember.Title = (MemberTitle)Convert.ToInt32(Console.ReadLine());
                    Console.Write("\n");

                    Console.Write("First Name: ");
                    newMember.FirstName = Convert.ToString(Console.ReadLine());
                    Console.Write("\n");

                    Console.Write("Last Name: ");
                    newMember.LastName = Convert.ToString(Console.ReadLine());
                    Console.Write("\n");

                    Console.Write("Member Type: ");
                    newMember.Type = (MemberType)Convert.ToInt32(Console.ReadLine());
                    Console.Write("\n");

                    Console.WriteLine("-----------------------------------------------------------------------");
                    Console.Write("Are you sure to add this customer? (Y/N): ");
                    addConfirmation = Convert.ToChar(Console.ReadLine());

                    if (addConfirmation.Equals('Y'))
                    {
                        if (newMember.Add())
                        {
                            Console.Write("New Customer is added successfully. Do you want to add more customers? (Y/N): ");
                            newEntryConfirmation = Convert.ToChar(Console.ReadLine());
                            Console.Write("\n");
                        }
                    }

                } while (newEntryConfirmation.Equals('Y'));
            }
            catch
            {
                throw;
            }
        }

        public void GetAll()
        {
            try
            {
                Member newMember = new Member(@"D:\ParaCustomer.txt");
                List<Member> members = newMember.ViewAll();

                if (members != null && members.Count > 0)
                {

                    Console.WriteLine("-----------------------------------------------------------------------");
                    Console.WriteLine("Title\tFirst Name\tLast Name\tType");
                    Console.WriteLine("-----------------------------------------------------------------------");
                    foreach (Member member in members)
                    {
                        Console.WriteLine(string.Concat(member.Title.ToString(), "\t", member.FirstName, "\t", member.LastName, "\t", member.Type.ToString()));
                        Console.WriteLine("-----------------------------------------------------------------------");
                    }
                }
                else
                {
                    Console.WriteLine("-----------------------------------------------------------------------");
                    Console.Write("No Members found...!!!");
                    Console.WriteLine("-----------------------------------------------------------------------");
                }
            }
            catch
            {
                throw;
            }
        }

    }
}

--- user form---\using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SharesAccountingSystem
{
    internal class User
    {
    }
}
 
 
 --- enumerator---
 using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SharesBusiness
{
    public enum MemberTitle
    {
        Mr = 1,
        Mrs = 2,
        Mis = 3,
        Trust = 4,
        Pvt = 5,
        NGO = 6
    }

    public enum MemberType
    {
        Regular = 1,
        Nominal = 2
    }

}
