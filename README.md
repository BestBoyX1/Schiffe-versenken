namespace Schiffe_versenken
{
    internal class Program
    {
        static void Main(string[] args)
        {
            bool FE = false; // Falsche Eingabe
            int Sp = 1; //Spieler 
            int STS1 = 0; // SChiff Treffer Spieler 1
            int STS2 = 0; // SChiff Treffer Spieler 2

            string[,] S1SF = new string[11, 11];
            string[,] S2SF = new string[11, 11];
            string[,] S1AF = new string[11, 11];
            string[,] S2AF = new string[11, 11];

            for (int i = 0; i < 11; i++)
            {
                for (int j = 0; j < 11; j++)
                {
                    S1SF[i, j] = ".| ";
                    S2SF[i, j] = ".| ";
                    S1AF[i, j] = ".| ";
                    S2AF[i, j] = ".| ";
                }
                for (int j = 0; j < 11; j++)
                {
                    if (j == 0)
                    {
                        S1SF[i, 0] = i + "| ";
                        S2SF[i, 0] = i + "| ";
                        S1AF[i, 0] = i + "| ";
                        S2AF[i, 0] = i + "| ";
                    }
                    else if (i != 0)
                    {
                        S1SF[0, i] = i + "| ";
                        S2SF[0, i] = i + "| ";
                        S1AF[0, i] = i + "| ";
                        S2AF[0, i] = i + "| ";
                    }
                }
            }

            // Spieler 1 Schiffe plazieren | S2=4x2 S3=3x3 S4=2x4 S5=1x5
            for (int j = 1; j == 4; j++)
            {
                S2P(S1SF, 1);
            }
            for (int j = 1; j == 3; j++)
            {
                S3P(S1SF, 1);
            }
            for (int j = 1; j == 2; j++)
            {
                S4P(S1SF, 1);
            }
            for (int j = 1; j == 1; j++)
            {
                S5P(S1SF, 1);
            }

            Console.Clear();
            Console.ReadKey();

            // Spieler 2 Schiffe plazieren | S2=4x2 S3=3x3 S4=2x4 S5=1x5
            for (int j = 1; j == 4; j++)
            {
                S2P(S2SF, 1);
            }
            for (int j = 1; j == 3; j++)
            {
                S3P(S2SF, 1);
            }
            for (int j = 1; j == 2; j++)
            {
                S4P(S2SF, 1);
            }
            for (int j = 1; j == 1; j++)
            {
                S5P(S2SF, 1);
            }

            Console.Clear();
            Console.ReadKey();


            while (true)
            {

                // Zeile
                Console.WriteLine("Zeile eingeben");
                string ZStr = Console.ReadLine();

                if (!int.TryParse(ZStr, out int Z))
                {
                    Console.WriteLine("Ungültige eingabe, versuche es nochmal!");
                    continue;
                }


                // Spalte
                Console.WriteLine("Spalte eingeben");
                string SStr = Console.ReadLine();

                if (!int.TryParse(SStr, out int S))
                {
                    Console.WriteLine("Ungültige eingabe, versuche es nochmal!");
                    continue;
                }
                

                // Hauptprogramm







                // Gewinn Kontrolle
                if (GK(STS1) == true)
                {
                    
                    break;
                }
                else if (GK(STS2) == true)
                {
                    break;
                }

                // Spieler ändern
                if (Sp == 1)
                {
                    Sp = 2;
                }
                else
                {
                    Sp = 1;
                }
            }

            Console.WriteLine("---- ---- ---- ----");
            Console.WriteLine("Der Spieler " + Sp + " hat gewonnen!");
            Console.WriteLine("Das Spiel endet jetzt!");
            Console.WriteLine("---- ---- ---- ----");

        }

        static string[,] FA(string[,] SF) // Feld Anzeigen
        {
            for (int i = 0; i < 11; i++)
            {
                for (int j = 0; j < 11; j++)
                {
                    Console.Write("{0,4}", SF[i, j]);
                }
                Console.WriteLine();
                Console.WriteLine("-------------------------------------------");
            }
            return SF;
        }
        static string[,] S2P(string[,] A, int n) // Schiff 2 Plazieren
        {
            Console.WriteLine("---- ---- ---- ----");
            Console.WriteLine("Spieler " + n + " Plaziert das 2-er Schiff!");
            Console.WriteLine("---- ---- ---- ----");

            bool PR = false; // Plazier Richtung (false: Vertikal / true: Horizontal)
            int Z = 0;
            int S = 0;

            FA(A);

            while (true)
            {
                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Koordinate für Zeile eingeben:");
                string Zstr = Console.ReadLine();
                bool Zb = int.TryParse(Zstr, out Z);

                if (Zb == false)
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Koordinate für Spalte eingeben:");
                string Sstr = Console.ReadLine();
                bool Sb = int.TryParse(Sstr, out S);

                if (Sb == false)
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Richung aufstellen (false: Vertikal / true Horizontal):");
                string PRstr = Console.ReadLine();

                if (PRstr == "true")
                {
                    PR = true;
                }
                else if (PRstr == "false")
                {
                    PR = false;
                }
                else
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                if ((1 <= Z && Z <= 10 && 1 <= S && S <= 9 && PR) || (1 <= Z && Z <= 9 && 1 <= S && S <= 10 && !PR))
                {
                    if (!PR)
                    {
                        for (int i = 0; i < 2; i++)
                        {
                            A[(Z + i), S] = "S| ";
                        }
                    }
                    else
                    {
                        for (int i = 0; i < 2; i++)
                        {
                            A[Z, (S + i)] = "S| ";
                        }
                    }
                }
                else
                {
                    continue;
                }

                break;
            }
            return A;
        }
        static string[,] S3P(string[,] A, int n) // Schiff 3 Plazieren
        {
            Console.WriteLine("---- ---- ---- ----");
            Console.WriteLine("Spieler " + n + " Plaziert das 3-er Schiff!");
            Console.WriteLine("---- ---- ---- ----");

            bool PR = false; // Plazier Richtung (false: Vertikal / true: Horizontal)
            int Z = 0;
            int S = 0;

            FA(A);

            while (true)
            {
                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Koordinate für Zeile eingeben:");
                string Zstr = Console.ReadLine();
                bool Zb = int.TryParse(Zstr, out Z);

                if (Zb == false)
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Koordinate für Spalte eingeben:");
                string Sstr = Console.ReadLine();
                bool Sb = int.TryParse(Sstr, out S);

                if (Sb == false)
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Richung aufstellen (false: Vertikal / true Horizontal):");
                string PRstr = Console.ReadLine();

                if (PRstr == "true")
                {
                    PR = true;
                }
                else if (PRstr == "false")
                {
                    PR = false;
                }
                else
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                if ((1 <= Z && Z <= 10 && 1 <= S && S <= 8 && PR) || (1 <= Z && Z <= 8 && 1 <= S && S <= 10 && !PR))
                {
                    if (!PR)
                    {
                        for (int i = 0; i < 3; i++)
                        {
                            A[(Z + i), S] = "S| ";
                        }
                    }
                    else
                    {
                        for (int i = 0; i < 3; i++)
                        {
                            A[Z, (S + i)] = "S| ";
                        }
                    }
                }
                else
                {
                    continue;
                }

                break;
            }
            return A;
        }
        static string[,] S4P(string[,] A, int n) // Schiff 4 Plazieren
        {
            Console.WriteLine("---- ---- ---- ----");
            Console.WriteLine("Spieler " + n + " Plaziert das 3-er Schiff!");
            Console.WriteLine("---- ---- ---- ----");

            bool PR = false; // Plazier Richtung (false: Vertikal / true: Horizontal)
            int Z = 0;
            int S = 0;

            FA(A);

            while (true)
            {
                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Koordinate für Zeile eingeben:");
                string Zstr = Console.ReadLine();
                bool Zb = int.TryParse(Zstr, out Z);

                if (Zb == false)
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Koordinate für Spalte eingeben:");
                string Sstr = Console.ReadLine();
                bool Sb = int.TryParse(Sstr, out S);

                if (Sb == false)
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Richung aufstellen (false: Vertikal / true Horizontal):");
                string PRstr = Console.ReadLine();

                if (PRstr == "true")
                {
                    PR = true;
                }
                else if (PRstr == "false")
                {
                    PR = false;
                }
                else
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                if ((1 <= Z && Z <= 10 && 1 <= S && S <= 7 && PR) || (1 <= Z && Z <= 7 && 1 <= S && S <= 10 && !PR))
                {
                    if (!PR)
                    {
                        for (int i = 0; i < 4; i++)
                        {
                            A[(Z + i), S] = "S| ";
                        }
                    }
                    else
                    {
                        for (int i = 0; i < 4; i++)
                        {
                            A[Z, (S + i)] = "S| ";
                        }
                    }
                }
                else
                {
                    continue;
                }

                break;
            }
            return A;
        }
        static string[,] S5P(string[,] A, int n) // Schiff 5 Plazieren
        {
            Console.WriteLine("---- ---- ---- ----");
            Console.WriteLine("Spieler " + n + " Plaziert das 4-er Schiff!");
            Console.WriteLine("---- ---- ---- ----");

            bool PR = false; // Plazier Richtung (false: Vertikal / true: Horizontal)
            int Z = 0;
            int S = 0;

            FA(A);

            while (true)
            {
                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Koordinate für Zeile eingeben:");
                string Zstr = Console.ReadLine();
                bool Zb = int.TryParse(Zstr, out Z);

                if (Zb == false)
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Koordinate für Spalte eingeben:");
                string Sstr = Console.ReadLine();
                bool Sb = int.TryParse(Sstr, out S);

                if (Sb == false)
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                Console.WriteLine("---- ---- ---- ----");
                Console.WriteLine("Richung aufstellen (false: Vertikal / true Horizontal):");
                string PRstr = Console.ReadLine();

                if (PRstr == "true")
                {
                    PR = true;
                }
                else if (PRstr == "false")
                {
                    PR = false;
                }
                else
                {
                    Console.WriteLine("Falsche Eingabe, versuche es nochmal!");
                    continue;
                }

                if ((1 <= Z && Z <= 10 && 1 <= S && S <= 6 && PR) || (1 <= Z && Z <= 6 && 1 <= S && S <= 10 && !PR))
                {
                    if (!PR)
                    {
                        for (int i = 0; i < 5; i++)
                        {
                            A[(Z + i), S] = "S| ";
                        }
                    }
                    else
                    {
                        for (int i = 0; i < 5; i++)
                        {
                            A[Z, (S + i)] = "S| ";
                        }
                    }
                }
                else
                {
                    continue;
                }

                break;
            }
            return A;
        }
        static bool AK(string[,] AF, int Zeile, int Spalte) // Attacke Kontrolle
        {
            if (AF[Zeile, Spalte] != ".| ")
            {
                return false;
            }

            return true;
        }
        static bool GK(int ST) // Gewinn Kontrolle
        {
            if (ST == 30)
            {
                return true;
            }
            return false;
        }
    }
}
