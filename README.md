** This is the Table and Stored Procedure that i am using in this project. **
CREATE TABLE Products (
    ID UNIQUEIDENTIFIER PRIMARY KEY,
    Name NVARCHAR(100) NOT NULL,
    Description NVARCHAR(MAX),
    Price DECIMAL(18, 2) NOT NULL
);


CREATE PROCEDURE usp_InsertProduct
    @Name NVARCHAR(100),
    @Description NVARCHAR(MAX),
    @Price DECIMAL(18, 2),
    @InsertedId UNIQUEIDENTIFIER OUTPUT
AS
BEGIN
    DECLARE @NewId UNIQUEIDENTIFIER;
    SET @NewId = NEWID();

    INSERT INTO Products (ID, Name, Description, Price)
    VALUES (@NewId, @Name, @Description, @Price);

    SET @InsertedId = @NewId;
END;




CREATE PROCEDURE usp_UpdateProduct
    @ID UNIQUEIDENTIFIER,
    @Name NVARCHAR(100),
    @Description NVARCHAR(MAX),
    @Price DECIMAL(18, 2)
AS
BEGIN
    UPDATE Products
    SET Name = @Name, Description = @Description, Price = @Price
    WHERE ID = @ID;
END;


CREATE PROCEDURE usp_GetProducts
AS
BEGIN
    SELECT ID, Name, Description, Price FROM Products;
END;


CREATE PROCEDURE usp_GetProductById
    @ID UNIQUEIDENTIFIER
AS
BEGIN
    SELECT ID, Name, Description, Price FROM Products
    WHERE ID = @ID;
END;


CREATE PROCEDURE usp_DeleteProduct
    @ID UNIQUEIDENTIFIER
AS
BEGIN
    DELETE FROM Products
    WHERE ID = @ID;
END;


SELECT * FROM Products
