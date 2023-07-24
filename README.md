<h1 align="center">Hi 👋, I'm Benjamin Clark</h1>
<h3 align="center">A DevOps Engineer based in Cambridge</h3>

```python
# Standard modules
from abc import ABC
from abc import abstractmethod
from dataclasses import dataclass, field
from datetime import datetime
from typing import List

# Constants
CURRENT_YEAR = datetime.now().year


class IHuman(ABC):
    """
    Baseline Human abstract
    """

    @abstractmethod
    def _get_age(self) -> int:
        """
        Return how old this human is

        :return: How old this human is
        """
        raise NotImplementedError

    @abstractmethod
    def _get_name(self) -> str:
        """
        Return what this human calls themselves

        :return: What this human calls themselves.
        """
        raise NotImplementedError

    def __str__(self) -> str:
        """
        Overwritten string method

        :return: Informal string representation of this object
        """
        return f"Name: {self._get_name()}, Age: {self._get_age()}"

    def __hash__(self) -> int:
        """
        Overwritten hash method

        :return: Int representation of this object that is unique
        """
        return hash((self._get_age(), self._get_name()))

    def __eq__(self, other) -> bool:
        """
        Method to determine if two instances are equal or not

        :param other: other object to compare to

        :return: True if instances are equal, otherwise False
        """
        if not isinstance(other, type(self)):
            return False
        return self._get_age() == other._get_age() and self._get_name() == other._get_name()


@dataclass
class SoftwareEngineer(IHuman):
    """
    Representation of a computer nerd who lives in baselines and jams with console cowboys in cyberspace
    """
    name: str
    age: int
    years_of_experience: int
    known_languages: List[str] = field(default_factory=list)

    def _get_age(self): return self.age

    def _get_name(self): return self.name

    def knows_language(self, language) -> bool:
        """
        Determine if the Engineer knows the input language or not

        :param language: Language which we wish to check if the Engineer knows
        :return: True if Engineer knows this language, else False
        """
        return language in self.known_languages


my_name = "Benjamin Clark"
date_of_birth = 1995
my_age = CURRENT_YEAR - date_of_birth

first_working_year = 2013
my_years_of_experience = CURRENT_YEAR - first_working_year

my_known_languages = [
    "Python",
    "C-Sharp",
    "Java",
    "HTML",
    "CSS",
    "JS",
    "Bash",
    "PowerShell"
]

me = SoftwareEngineer(
    name=my_name,
    age=my_age,
    years_of_experience=my_years_of_experience,
    known_languages=my_known_languages
)

valid_input = False
recruiter = None
while not valid_input:
    is_recruiter = input("Are you a recruiter? Yes/No: ")
    if is_recruiter.lower() in ["yes", "no"]:
        valid_input = True
        recruiter = True if is_recruiter.lower() == "yes" else False
    else:
        print("Invalid input, please answer Yes/No\n")

if recruiter:
    message = [
        f"Hello! I'm {me.name}, an experienced Contract DevOps/Software Engineer with {me.years_of_experience} years of experience.",
        "If you can read the above, and not mistake any of the languages I know for a Pokemon, then maybe we should talk.",
        "But, uh, 99% of the code I write is private IP for my clients so take my GitHub with a pinch of salt.",
        "Contact me on my LinkedIn (Benni) or send enquiries to enquiries@sudoblark.com"
    ]
    print("\n".join(message))
```
