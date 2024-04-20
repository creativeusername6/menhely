#include <iostream>
#include <fstream>

struct menhely
{
    std::string faj;
    std::string nev;
    int kor;
    std::string szin;
    menhely* next;
};

menhely* adat(menhely* head, std::string faj, std::string nev, int kor, std::string szin)
{
    menhely* uj = new menhely;
    uj->faj = faj;
    uj->nev = nev;
    uj->kor = kor;
    uj->szin = szin;
    uj->next = NULL;
    if (head == NULL)
    {
        head = uj;
        return head;
    }
    menhely* temp = head;
    while (temp->next != NULL)
    {
        temp = temp->next;
    }
    temp->next = uj;
    return head;
}

int main()
{
    std::ifstream file(/*beolvasandó fájl*/);

    menhely* head = NULL;
    std::string faj;
    std::string nev;
    int kor;
    std::string szin;
    int kereses;
    char ujr;
    bool ujra = true;
    int loop;
    
    while (file >> faj >> nev >> kor >> szin)
    {
        head = adat(head, faj, nev, kor, szin);
    }

    while (ujra)
    {
        ujr = ' ';
        kereses = 0;
        loop = 0;
        while (kereses < 1 or kereses > 4)
        {
            std::cout << "Mi alapjan szeretne keresni?" << std::endl;
            std::cout << "1: faj" << std::endl;
            std::cout << "2: nev" << std::endl;
            std::cout << "3: kor" << std::endl;
            std::cout << "4: szin" << std::endl;
            std::cin >> kereses;
        }

        menhely* temp = head;
        switch (kereses)
        {
        case 1:
            std::cout << "Keresett fajta?" << std::endl;
            std::cin >> faj;
            while (temp != NULL)
            {
                if (faj == temp->faj)
                {
                    std::cout << temp->faj << " " << temp->nev << " " << temp->kor << " " << temp->szin << std::endl;
                    loop++;
                }
                temp = temp->next;
            }
            if (loop == 0)
            {
                std::cout << "Nem volt ilyen allat" << std::endl;
            }
            break;
        case 2:
            std::cout << "Keresett nev?" << std::endl;
            std::cin >> nev;
            while (temp != NULL)
            {
                if (nev == temp->nev)
                {
                    std::cout << temp->faj << " " << temp->nev << " " << temp->kor << " " << temp->szin << std::endl;
                    loop++;
                }
                temp = temp->next;
            }
            if (loop == 0)
            {
                std::cout << "Nem volt ilyen allat" << std::endl;
            }
            break;
        case 3:
            std::cout << "Keresett kor?" << std::endl;
            std::cin >> kor;
            while (temp != NULL)
            {
                if (kor == temp->kor)
                {
                    std::cout << temp->faj << " " << temp->nev << " " << temp->kor << " " << temp->szin << std::endl;
                    loop++;
                }
                temp = temp->next;
            }
            if (loop == 0)
            {
                std::cout << "Nem volt ilye allat" << std::endl;
            }
            break;
        case 4:
            std::cout << "Keresett szin?" << std::endl;
            std::cin >> szin;
            while (temp != NULL)
            {
                if (szin == temp->szin)
                {
                    std::cout << temp->faj << " " << temp->nev << " " << temp->kor << " " << temp->szin << std::endl;
                    loop++;
                }
                temp = temp->next;
            }
            if (loop == 0)
            {
                std::cout << "Nem volt ilyen allat" << std::endl;
            }
            break;
        default:
            break;
        }
        std::cout << "Ujra?(i/n)" << std::endl;
        while ((ujr != 'i') and (ujr != 'n'))
        {
            std::cin >> ujr;
            if (ujr == 'n')
            {
                ujra = false;
            }
        }
    }

    menhely* akt = head;
    while (akt != NULL)
    {
        menhely* temp2 = akt->next;
        delete(akt);
        akt = temp2;
    }
}
