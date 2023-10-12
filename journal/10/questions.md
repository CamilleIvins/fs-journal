# CSharp and SQL Fundamentals
01. What is the purpose of a `namespace`?

  > | 'namespace' is used to control classes throughout an application. They also organize how elements are presented to programs with which they interact. |

02. What is the difference between a `class` and an `interface`?

  > | Interface relates to how functionality plays out, while classes have more direct control of what will happen, and the control over triggering the actions. |

03. What is the method that returns an instance of a class, yet it has no return type?

  > | Is this the task? I may be a little confused on this point, but this is related to how we managed collaborators in C# Post-It. |

05. In the Car example what is the access modifier of the `Start()` method?

  ```c#
  abstract class Car
  {
    public string Start()
    {

      return "Vroooom";

    }
  }
  ```

  > | 'public'? |

06. In the Car example what is `string` an indication of?

  > | How the data is stored - what type of information it is. |

07. In the Car example what is `abstract` preventing?

  > | I think the abstraction is limiting the actual entry into functions, as it is not the class directly acted upon. So it is the base controller equivalent, with no direct access by users to ever have the data manipulated. |

08. In a SQL table, what is the difference between information in a row and information in a column?

  > | Information in rows belong to a single instance, whereas columns contain the data across instances for a single value type. |

09. Demonstrate the necessary SQL for creating a table called `characters` with the values `name, age, description` as strings, and an `int` id.

  > | CREATE TABLE
    characters(
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR (500),
        age VARCHAR(50),
        description VARCHAR(1000),
    ); |

10. In SQL how can you query more than a single table? Provide an example.

  > | The data provided is a Super Stellar Instructor Sam original:

      internal List<Picture> GetPicturesByAlbumId(int albumId)
    {
        string sql = @"
        SELECT
        pic.*,
        act.*
        FROM pictures pic
        JOIN accounts act ON act.id = pic.creatorId
        WHERE albumId = @albumId
        ;";
        List<Picture> pictures = _db.Query<Picture, Account, Picture>(sql, (picture, account) =>
        {
            picture.Creator = account;
            return picture;
        }, new { albumId }).ToList();
        return pictures;
    }

   An element of what is going on here is that the two tables are being accessed in the first two entries into the query, while their relevent subject is the third, and final, portion. |
