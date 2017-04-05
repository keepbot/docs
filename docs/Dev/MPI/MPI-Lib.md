### MPI_Abort.md
```
MPI_Abort(3)                          MPI                         MPI_Abort(3)



NAME
       MPI_Abort -  Terminates MPI execution environment

SYNOPSIS
       #include "mpi.h"
       int MPI_Abort( MPI_Comm comm, int errorcode )

INPUT PARAMETERS
       comm   - communicator of tasks to abort
       errorcode
              - error code to return to invoking environment


NOTES
       Terminates all MPI processes associated with the communicator comm ; in
       most systems (all to date), terminates all processes.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       abort.c



                                  12/13/2001                      MPI_Abort(3)
```

### MPI_Address.md
```
MPI_Address(3)                        MPI                       MPI_Address(3)



NAME
       MPI_Address -  Gets the address of a location in memory

SYNOPSIS
       #include "mpi.h"
       int MPI_Address( void *location, MPI_Aint *address)

INPUT PARAMETERS
       location
              - location in caller memory (choice)


OUTPUT PARAMETER
       address
              - address of location (integer)


NOTE
       This  routine  is  provided for both the Fortran and C programmers.  On
       many systems, the address returned by this routine will be the same  as
       produced by the C & operator, but this is not required in C and may not
       be true of systems with word- rather than byte-oriented instructions or
       systems with segmented address spaces.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       address.c



                                  11/14/2001                    MPI_Address(3)
```

### MPI_Allgather.md
```
MPI_Allgather(3)                      MPI                     MPI_Allgather(3)



NAME
       MPI_Allgather  -   Gathers data from all tasks and distribute it to all
       tasks

SYNOPSIS
       #include "mpi.h"
       int MPI_Allgather ( void *sendbuf, int sendcount, MPI_Datatype sendtype,
                           void *recvbuf, int recvcount, MPI_Datatype recvtype,
                          MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - starting address of send buffer (choice)
       sendcount
              - number of elements in send buffer (integer)
       sendtype
              - data type of send buffer elements (handle)
       recvcount
              - number of elements received from any process (integer)
       recvtype
              - data type of receive buffer elements (handle)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - address of receive buffer (choice)


NOTES
       The MPI standard (1.0 and 1.1) says that

       The jth block of data sent from each proess is received by  every  pro-
       cess and placed in the jth block of the buffer recvbuf .


       This is misleading; a better description is

       The  block  of data sent from the jth process is received by every pro-
       cess and placed in the jth block of the buffer recvbuf .


       This text was suggested by Rajeev Thakur.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler  may  be  changed  with  MPI_Errhandler_set  ;  the
       predefined error handler MPI_ERRORS_RETURN may be used to  cause  error
       values  to  be  returned.  Note that MPI does not guarentee that an MPI
       program can continue past an error.

       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              -  Invalid  buffer  pointer.  Usually a null buffer where one is
              not valid.

LOCATION
       allgather.c



                                   10/1/2004                  MPI_Allgather(3)
```

### MPI_Allgatherv.md
```
MPI_Allgatherv(3)                     MPI                    MPI_Allgatherv(3)



NAME
       MPI_Allgatherv -  Gathers data from all tasks and deliver it to all

SYNOPSIS
       #include "mpi.h"
       int MPI_Allgatherv ( void *sendbuf, int sendcount, MPI_Datatype sendtype,
                            void *recvbuf, int *recvcounts, int *displs,
                           MPI_Datatype recvtype, MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - starting address of send buffer (choice)
       sendcount
              - number of elements in send buffer (integer)
       sendtype
              - data type of send buffer elements (handle)
       recvcounts
              -  integer array (of length group size) containing the number of
              elements that are received from each process
       displs - integer array (of length group size). Entry  i  specifies  the
              displacement (relative to recvbuf ) at which to place the incom-
              ing data from process i

       recvtype
              - data type of receive buffer elements (handle)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - address of receive buffer (choice)


NOTES
       The MPI standard (1.0 and 1.1) says that

       The jth block of data sent from each proess is received by  every  pro-
       cess and placed in the jth block of the buffer recvbuf .


       This is misleading; a better description is

       The  block  of data sent from the jth process is received by every pro-
       cess and placed in the jth block of the buffer recvbuf .


       This text was suggested by Rajeev Thakur.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_ERR_BUFFER
              - Invalid buffer pointer.  Usually a null buffer  where  one  is
              not valid.
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).

LOCATION
       allgatherv.c



                                  11/14/2001                 MPI_Allgatherv(3)
```

### MPI_Allreduce.md
```
MPI_Allreduce(3)                      MPI                     MPI_Allreduce(3)



NAME
       MPI_Allreduce  -  Combines values from all processes and distribute the
       result back to all processes

SYNOPSIS
       #include "mpi.h"
       int MPI_Allreduce ( void *sendbuf, void *recvbuf, int count,
                          MPI_Datatype datatype, MPI_Op op, MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - starting address of send buffer (choice)
       count  - number of elements in send buffer (integer)
       datatype
              - data type of elements of send buffer (handle)
       op     - operation (handle)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - starting address of receive buffer (choice)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


NOTES ON COLLECTIVE OPERATIONS
       The  reduction functions ( MPI_Op ) do not return an error value.  As a
       result, if the functions detect an error, all they  can  do  is  either
       call  MPI_Abort  or silently skip the problem.  Thus, if you change the
       error handler from MPI_ERRORS_ARE_FATAL to something else, for example,
       MPI_ERRORS_RETURN , then no error may be indicated.

       The  reason  for  this is the performance problems in ensuring that all
       collective routines return the same error value.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_ERR_BUFFER
              -  Invalid  buffer  pointer.  Usually a null buffer where one is
              not valid.
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_OP
              - Invalid operation.  MPI operations (objects of type  MPI_Op  )
              must either be one of the predefined operations (e.g., MPI_SUM )
              or created with MPI_Op_create .

       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).

LOCATION
       allreduce.c



                                  11/14/2001                  MPI_Allreduce(3)
```

### MPI_Alltoall.md
```
MPI_Alltoall(3)                       MPI                      MPI_Alltoall(3)



NAME
       MPI_Alltoall -  Sends data from all to all processes

SYNOPSIS
       #include "mpi.h"
       int MPI_Alltoall( void *sendbuf, int sendcount, MPI_Datatype sendtype,
                         void *recvbuf, int recvcnt, MPI_Datatype recvtype,
                        MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - starting address of send buffer (choice)
       sendcount
              - number of elements to send to each process (integer)
       sendtype
              - data type of send buffer elements (handle)
       recvcount
              - number of elements received from any process (integer)
       recvtype
              - data type of receive buffer elements (handle)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - address of receive buffer (choice)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              - Invalid buffer pointer.  Usually a null buffer  where  one  is
              not valid.

LOCATION
       alltoall.c



                                  11/14/2001                   MPI_Alltoall(3)
```

### MPI_Alltoallv.md
```
MPI_Alltoallv(3)                      MPI                     MPI_Alltoallv(3)



NAME
       MPI_Alltoallv -  Sends data from all to all processes, with a displace-
       ment

SYNOPSIS
       #include "mpi.h"
       int MPI_Alltoallv (
               void *sendbuf,
               int *sendcnts,
               int *sdispls,
               MPI_Datatype sendtype,
               void *recvbuf,
               int *recvcnts,
               int *rdispls,
               MPI_Datatype recvtype,
               MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - starting address of send buffer (choice)
       sendcounts
              - integer array equal to the group size specifying the number of
              elements to send to each processor
       sdispls
              -  integer  array  (of length group size). Entry j specifies the
              displacement (relative to sendbuf  from which to take the outgo-
              ing data destined for process j

       sendtype
              - data type of send buffer elements (handle)
       recvcounts
              -  integer  array equal to the group size specifying the maximum
              number of elements that can be received from each processor
       rdispls
              - integer array (of length group size). Entry  i  specifies  the
              displacement  (relative to recvbuf  at which to place the incom-
              ing data from process i

       recvtype
              - data type of receive buffer elements (handle)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - address of receive buffer (choice)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              -  Invalid  buffer  pointer.  Usually a null buffer where one is
              not valid.

LOCATION
       alltoallv.c



                                  11/14/2001                  MPI_Alltoallv(3)
```

### MPI_Attr_delete.md
```
MPI_Attr_delete(3)                    MPI                   MPI_Attr_delete(3)



NAME
       MPI_Attr_delete -  Deletes attribute value associated with a key

SYNOPSIS
       #include "mpi.h"
       int MPI_Attr_delete ( MPI_Comm comm, int keyval )

INPUT PARAMETERS
       comm   - communicator to which attribute is attached (handle)
       keyval - The key value of the deleted attribute (integer)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - This error class is associated with an error code  that  indi-
              cates  that  an  attempt  was  made to free one of the permanent
              keys.

LOCATION
       attr_delval.c



                                  11/14/2001                MPI_Attr_delete(3)
```

### MPI_Attr_get.md
```
MPI_Attr_get(3)                       MPI                      MPI_Attr_get(3)



NAME
       MPI_Attr_get -  Retrieves attribute value by key

SYNOPSIS
       #include "mpi.h"
       int MPI_Attr_get (
               MPI_Comm comm,
               int keyval,
               void *attr_value,
               int *flag )

INPUT PARAMETERS
       comm   - communicator to which attribute is attached (handle)
       keyval - key value (integer)


OUTPUT PARAMETERS
       attr_value
              - attribute value, unless flag = false
       flag   -  true  if  an  attribute  value  was  extracted;   false if no
              attribute is associated with the key


NOTES
       Attributes must be extracted  from  the  same  language  as  they  were
       inserted  in  with  MPI_ATTR_PUT  .   The notes for C and Fortran below
       explain why.


NOTES FOR C
       Even though the attr_value arguement is declared as  void  *  ,  it  is
       really  the  address of a void pointer.  See the rationale in the stan-
       dard for more details.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

       The  attr_value  in  Fortran  is  a pointer to a Fortran integer, not a
       pointer to a void * .



ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_OTHER
              - Other error; the error code associated with this  error  indi-
              cates an attempt to use an invalue keyval.

LOCATION
       attr_getval.c



                                  11/14/2001                   MPI_Attr_get(3)
```

### MPI_Attr_put.md
```
MPI_Attr_put(3)                       MPI                      MPI_Attr_put(3)



NAME
       MPI_Attr_put -  Stores attribute value associated with a key

SYNOPSIS
       #include "mpi.h"
       int MPI_Attr_put ( MPI_Comm comm, int keyval, void *attr_value )

INPUT PARAMETERS
       comm   - communicator to which attribute will be attached (handle)
       keyval - key value, as returned by MPI_KEYVAL_CREATE (integer)
       attribute_val
              - attribute value


NOTES
       Values of the permanent attributes MPI_TAG_UB , MPI_HOST , MPI_IO , and
       MPI_WTIME_IS_GLOBAL may not be changed.

       The type of the attribute value depends on  whether  C  or  Fortran  is
       being  used.  In C, an attribute value is a pointer ( void * ); in For-
       tran, it is a single integer ( not a  pointer,  since  Fortran  has  no
       pointers  and  there are systems for which a pointer does not fit in an
       integer (e.g., any > 32 bit address system that uses 64 bits  for  For-
       tran DOUBLE PRECISION ).

       If an attribute is already present, the delete function (specified when
       the corresponding keyval was created) will be called.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_OTHER
              -  Other  error; the error code associated with this error indi-
              cates an attempt to use an invalue keyval.
       MPI_ERR_ARG
              - This error class is associated with an error code  that  indi-
              cates  that  an  attempt  was  made to free one of the permanent
              keys.


SEE ALSO
       MPI_Attr_get, MPI_Keyval_create, MPI_Attr_delete

LOCATION
       attr_putval.c



                                  11/14/2001                   MPI_Attr_put(3)
```

### MPI_Barrier.md
```
MPI_Barrier(3)                        MPI                       MPI_Barrier(3)



NAME
       MPI_Barrier -  Blocks until all process have reached this routine.

SYNOPSIS
       #include "mpi.h"
       int MPI_Barrier (
               MPI_Comm comm )

INPUT PARAMETERS
       comm   - communicator (handle)


NOTES
       Blocks  the  caller  until  all  group members have called it; the call
       returns at any process only after all group members  have  entered  the
       call.


ALGORITHM
       If the underlying device cannot do better, a tree-like or combine algo-
       rithm is used to broadcast a message wto all members of the  communica-
       tor.   We  can  modifiy  this  to  use  "blocks"  at  a later time (see
       MPI_Bcast ).


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).

LOCATION
       barrier.c



                                  11/14/2001                    MPI_Barrier(3)
```

### MPI_Bcast.md
```
MPI_Bcast(3)                          MPI                         MPI_Bcast(3)



NAME
       MPI_Bcast  -  Broadcasts a message from the process with rank "root" to
       all other processes of the group.

SYNOPSIS
       #include "mpi.h"
       int MPI_Bcast ( void *buffer, int count, MPI_Datatype datatype, int root,
                      MPI_Comm comm )

INPUT/OUTPUT PARAMETERS
       buffer - starting address of buffer (choice)
       count  - number of entries in buffer (integer)
       datatype
              - data type of buffer (handle)
       root   - rank of broadcast root (integer)
       comm   - communicator (handle)


ALGORITHM
       If the underlying device does not take  responsibility,  this  function
       uses  a  tree-like algorithm to broadcast the message to blocks of pro-
       cesses.  A linear algorithm is then used to broadcast the message  from
       the    first   process   in   a   block   to   all   other   processes.
       MPIR_BCAST_BLOCK_SIZE determines the size of blocks.  If this is set to
       1, then this function is equivalent to using a pure tree algorithm.  If
       it is set to the size of the group or greater,  it  is  a  pure  linear
       algorithm.   The  value  should be adjusted to determine the most effi-
       cient value on different machines.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              -  Invalid  buffer  pointer.  Usually a null buffer where one is
              not valid.
       MPI_ERR_ROOT
              - Invalid root.  The root must be specified as  a  rank  in  the
              communicator.   Ranks  must  be between zero and the size of the
              communicator minus one.

LOCATION
       bcast.c



                                  11/14/2001                      MPI_Bcast(3)
```

### MPI_Bsend_init.md
```
MPI_Bsend_init(3)                     MPI                    MPI_Bsend_init(3)



NAME
       MPI_Bsend_init -  Builds a handle for a buffered send

SYNOPSIS
       #include "mpi.h"
       int MPI_Bsend_init( void *buf, int count, MPI_Datatype datatype, int dest,
                          int tag, MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements sent (integer)
       datatype
              - type of each element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_RANK
              - Invalid source or destination rank.   Ranks  must  be  between
              zero  and  the  size  of  the communicator minus one; ranks in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_SOURCE .

       MPI_ERR_TAG
              -  Invalid  tag  argument.  Tags must be non-negative; tags in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .


LOCATION
       bsend_init.c



                                  12/13/2001                 MPI_Bsend_init(3)
```

### MPI_Bsend.md
```
MPI_Bsend(3)                          MPI                         MPI_Bsend(3)



NAME
       MPI_Bsend -  Basic send with user-specified buffering

SYNOPSIS
       #include "mpi.h"
       int MPI_Bsend(
               void *buf,
               int count,
               MPI_Datatype datatype,
               int dest,
               int tag,
               MPI_Comm comm )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements in send buffer (nonnegative integer)
       datatype
              - datatype of each send buffer element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


NOTES
       This  send is provided as a convenience function; it allows the user to
       send messages without worring about where they  are  buffered  (because
       the user must have provided buffer space with MPI_Buffer_attach ).

       In deciding how much buffer space to allocate, remember that the buffer
       space is not available for reuse by subsequent MPI_Bsend s  unless  you
       are certain that the message has been received (not just that it should
       have been received).  For example, this code does not  allocate  enough
       buffer space
       MPI_Buffer_attach( b, n*sizeof(double) + MPI_BSEND_OVERHEAD );
       for (i=0; i<m; i++) {
       MPI_Bsend( buf, n, MPI_DOUBLE, ... );
       }

       because only enough buffer space is provided for a single send, and the
       loop may start a second MPI_Bsend before the first is done  making  use
       of the buffer.

       In C, you can force the messages to be delivered by
       MPI_Buffer_detach( &b, &n );
       MPI_Buffer_attach( b, n );

       (The  MPI_Buffer_detach  will  not complete until all buffered messages
       are delivered.)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .



SEE ALSO
       MPI_Buffer_attach, MPI_Ibsend, MPI_Bsend_init

LOCATION
       bsend.c



                                  11/14/2001                      MPI_Bsend(3)
```

### MPI_Buffer_attach.md
```
MPI_Buffer_attach(3)                  MPI                 MPI_Buffer_attach(3)



NAME
       MPI_Buffer_attach -  Attaches a user-defined buffer for sending

SYNOPSIS
       #include "mpi.h"
       int MPI_Buffer_attach( void *buffer, int size )

INPUT PARAMETERS
       buffer - initial buffer address (choice)
       size   - buffer size, in bytes (integer)


NOTES
       The size given should be the sum of the sizes of all outstanding Bsends
       that you intend to have, plus a few hundred bytes for each  Bsend  that
       you  do.   For  the  purposes  of  calculating  size,  you  should  use
       MPI_Pack_size .

       In other words, in the code
       MPI_Buffer_attach( buffer, size );
       MPI_Bsend( ..., count=20, datatype=type1,  ... );
       .
       .
       .
       MPI_Bsend( ..., count=40, datatype=type2, ... );

       the value of size in the MPI_Buffer_attach call should be greater  than
       the value computed by
       MPI_Pack_size( 20, type1, comm, &s1 );
       MPI_Pack_size( 40, type2, comm, &s2 );
       size = s1 + s2 + 2 * MPI_BSEND_OVERHEAD;

       The  MPI_BSEND_OVERHEAD  gives  the maximum amount of space that may be
       used in the buffer for use by the BSEND routines in using  the  buffer.
       This value is in mpi.h (for C) and mpif.h (for Fortran).


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_BUFFER
              -  Invalid  buffer  pointer.  Usually a null buffer where one is
              not valid.
       MPI_ERR_INTERN
              - An internal error has been detected.  This is  fatal.   Please
              send a bug report to mpi-bugs@mcs.anl.gov .



SEE ALSO
       MPI_Buffer_detach, MPI_Bsend

LOCATION
       bufattach.c



                                  11/14/2001              MPI_Buffer_attach(3)
```

### MPI_Buffer_detach.md
```
MPI_Buffer_detach(3)                  MPI                 MPI_Buffer_detach(3)



NAME
       MPI_Buffer_detach  -   Removes an existing buffer (for use in MPI_Bsend
       etc)

SYNOPSIS
       #include "mpi.h"
       int MPI_Buffer_detach(
               void *bufferptr,
               int *size )

OUTPUT PARAMETERS
       buffer - initial buffer address (choice)
       size   - buffer size, in bytes (integer)


NOTES
       The reason that MPI_Buffer_detach returns the address and size  of  the
       buffer  being  detached  is  to  allow  nested libraries to replace and
       restore the buffer.  For example, consider

       int size, mysize, idummy;
       void *ptr, *myptr, *dummy;
       MPI_Buffer_detach( &ptr, &size );
       MPI_Buffer_attach( myptr, mysize );
       .
       .
       .
       .
       .
       .
       library code ...
       .
       .
       .
       MPI_Buffer_detach( &dummy, &idummy );
       MPI_Buffer_attach( ptr, size );


       This is much like the action of the Unix signal  routine  and  has  the
       same  strengths (it is simple) and weaknesses (it only works for nested
       usages).

       Note that for this approach  to  work,  MPI_Buffer_detach  must  return
       MPI_SUCCESS  even  when there is no buffer to detach.  In that case, it
       returns a size of zero.  The MPI  1.1  standard  for  MPI_BUFFER_DETACH
       contains the text

       The statements made in this section describe the behavior of MPI for
       buffered-mode sends. When no buffer is currently associated, MPI behaves
       as if a zero-sized buffer is associated with the process.


       This  could  be  read  as  applying only to the various Bsend routines.
       This  implementation  takes  the  position   that   this   applies   to
       MPI_BUFFER_DETACH as well.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

       The Fortran binding for this routine  is  different.   Because  Fortran
       does  not  have  pointers, it is impossible to provide a way to use the
       output of this routine to exchange buffers.  In  this  case,  only  the
       size field is set.


NOTES FOR C
       Even though the bufferptr argument is declared as void * , it is really
       the address of a void pointer.  See the rationale in the  standard  for
       more details.

LOCATION
       buffree.c



                                  11/14/2001              MPI_Buffer_detach(3)
```

### MPI_Cancel.md
```
MPI_Cancel(3)                         MPI                        MPI_Cancel(3)



NAME
       MPI_Cancel -  Cancels a communication request

SYNOPSIS
       #include "mpi.h"
       int MPI_Cancel( MPI_Request *request )

INPUT PARAMETER
       request
              - communication request (handle)


NOTE
       Cancel  has  only  been implemented for receive requests; it is a no-op
       for send requests.  The primary expected use of MPI_Cancel is in multi-
       buffering  schemes,  where  speculative  MPI_Irecvs are made.  When the
       computation completes, some of these receive requests may remain; using
       MPI_Cancel allows the user to cancel these unsatisfied requests.

       Cancelling  a  send  operation  is  much  more difficult, in large part
       because the send will usually  be  at  least  partially  complete  (the
       information  on  the tag, size, and source are usually sent immediately
       to the destination).  As of version 1.2.0, MPICH supports cancelling of
       sends.   Users are advised that cancelling a send, while a local opera-
       tion (as defined by the MPI standard), is likely to be expensive  (usu-
       ally generating one or more internal messages).


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


NULL HANDLES
       The MPI 1.1 specification, in the section on opaque objects, explicitly

DISALLOWS FREEING A NULL COMMUNICATOR. THE TEXT FROM THE STANDARD IS
       A null handle argument is an erroneous IN argument in MPI calls, unless an
       exception is explicitly stated in the text that defines the function. Such
       exception is allowed for handles to request objects in Wait and Test calls
       (sections Communication Completion and Multiple Completions ). Otherwise, a
       null handle can only be passed to a function that allocates a new object and
       returns a reference to it in the handle.



ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_REQUEST
              - Invalid MPI_Request .  Either  null  or,  in  the  case  of  a
              MPI_Start or MPI_Startall , not a persistent request.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       cancel.c



                                  11/14/2001                     MPI_Cancel(3)
```

### MPI_Cart_coords.md
```
MPI_Cart_coords(3)                    MPI                   MPI_Cart_coords(3)



NAME
       MPI_Cart_coords  -   Determines  process  coords  in cartesian topology
       given rank in group

SYNOPSIS
       #include "mpi.h"
       int MPI_Cart_coords ( MPI_Comm comm, int rank, int maxdims, int *coords )

INPUT PARAMETERS
       comm   - communicator with cartesian structure (handle)
       rank   - rank of a process within group of comm (integer)
       maxdims
              - length of vector coords in the calling program (integer)


OUTPUT PARAMETER
       coords - integer array (of size ndims ) containing the Cartesian  coor-
              dinates of specified process (integer)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_DIMS
              - Illegal dimension argument.  A dimension argument is  null  or
              its length is less than or equal to zero.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).


LOCATION
       cart_coords.c



                                   3/28/2002                MPI_Cart_coords(3)
```

### MPI_Cart_create.md
```
MPI_Cart_create(3)                    MPI                   MPI_Cart_create(3)



NAME
       MPI_Cart_create  -  Makes a new communicator to which topology informa-
       tion has been attached

SYNOPSIS
       #include "mpi.h"
       int MPI_Cart_create ( MPI_Comm comm_old, int ndims, int *dims, int *periods,
                            int reorder, MPI_Comm *comm_cart )

INPUT PARAMETERS
       comm_old
              - input communicator (handle)
       ndims  - number of dimensions of cartesian grid (integer)
       dims   - integer array of size ndims specifying the number of processes
              in each dimension
       periods
              -  logical  array  of  size ndims specifying whether the grid is
              periodic (true) or not (false) in each dimension
       reorder
              - ranking may be reordered (true) or not (false) (logical)


OUTPUT PARAMETER
       comm_cart
              - communicator with new cartesian topology (handle)


ALGORITHM
       We ignore reorder info currently.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_DIMS
              - Illegal dimension argument.  A dimension argument is  null  or
              its length is less than or equal to zero.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       cart_create.c



                                  11/14/2001                MPI_Cart_create(3)
```

### MPI_Cartdim_get.md
```
MPI_Cartdim_get(3)                    MPI                   MPI_Cartdim_get(3)



NAME
       MPI_Cartdim_get  -  Retrieves Cartesian topology information associated
       with a  communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Cartdim_get ( MPI_Comm comm, int *ndims )

INPUT PARAMETER
       comm   - communicator with cartesian structure (handle)


OUTPUT PARAMETER
       ndims  - number of dimensions of the cartesian structure (integer)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       cartdim_get.c



                                  11/14/2001                MPI_Cartdim_get(3)
```

### MPI_Cart_get.md
```
MPI_Cart_get(3)                       MPI                      MPI_Cart_get(3)



NAME
       MPI_Cart_get  -   Retrieves  Cartesian  topology information associated
       with a  communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Cart_get (
               MPI_Comm comm,
               int maxdims,
               int *dims,
               int *periods,
               int *coords )

INPUT PARAMETERS
       comm   - communicator with cartesian structure (handle)
       maxdims
              - length of vectors dims , periods , and coords in  the  calling
              program (integer)


OUTPUT PARAMETERS
       dims   -  number  of  processes  for each cartesian dimension (array of
              integer)
       periods
              - periodicity (true/false) for each cartesian  dimension  (array
              of logical)
       coords -  coordinates  of calling process in cartesian structure (array
              of integer)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       cart_get.c



                                  11/14/2001                   MPI_Cart_get(3)
```

### MPI_Cart_map.md
```
MPI_Cart_map(3)                       MPI                      MPI_Cart_map(3)



NAME
       MPI_Cart_map -  Maps process to Cartesian topology information

SYNOPSIS
       #include "mpi.h"
       int MPI_Cart_map (
               MPI_Comm comm_old,
               int ndims,
               int *dims,
               int *periods,
               int *newrank)

INPUT PARAMETERS
       comm   - input communicator (handle)
       ndims  - number of dimensions of Cartesian structure (integer)
       dims   - integer array of size ndims specifying the number of processes
              in each coordinate direction
       periods
              - logical array of size ndims specifying the periodicity  speci-
              fication in each coordinate direction


OUTPUT PARAMETER
       newrank
              -  reordered rank of the calling process; MPI_UNDEFINED if call-
              ing process does not belong to grid (integer)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_DIMS
              -  Illegal  dimension argument.  A dimension argument is null or
              its length is less than or equal to zero.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       cart_map.c



                                   3/28/2002                   MPI_Cart_map(3)
```

### MPI_Cart_rank.md
```
MPI_Cart_rank(3)                      MPI                     MPI_Cart_rank(3)



NAME
       MPI_Cart_rank  -   Determines process rank in communicator given Carte-
       sian location

SYNOPSIS
       #include "mpi.h"
       int MPI_Cart_rank (
               MPI_Comm comm,
               int *coords,
               int *rank )

INPUT PARAMETERS
       comm   - communicator with cartesian structure (handle)
       coords - integer array (of size ndims ) specifying the cartesian  coor-
              dinates of a process


OUTPUT PARAMETER
       rank   - rank of specified process (integer)


NOTES
       Out-of-range  coordinates  are  erroneous  for non-periodic dimensions.
       Versions of MPICH before 1.2.2 returned MPI_PROC_NULL for the  rank  in
       this case.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       cart_rank.c



                                  11/14/2001                  MPI_Cart_rank(3)
```

### MPI_Cart_shift.md
```
MPI_Cart_shift(3)                     MPI                    MPI_Cart_shift(3)



NAME
       MPI_Cart_shift  -   Returns  the  shifted source and destination ranks,
       given a  shift direction and amount

SYNOPSIS
       #include "mpi.h"
       int MPI_Cart_shift ( MPI_Comm comm, int direction, int displ,
                           int *source, int *dest )

INPUT PARAMETERS
       comm   - communicator with cartesian structure (handle)
       direction
              - coordinate dimension of shift (integer)
       disp   - displacement (> 0: upwards shift, < 0: downwards shift) (inte-
              ger)


OUTPUT PARAMETERS
       rank_source
              - rank of source process (integer)
       rank_dest
              - rank of destination process (integer)


NOTES
       The  direction  argument  is  in the range [0,n-1] for an n-dimensional
       Cartesian mesh.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       cart_shift.c



                                  11/14/2001                 MPI_Cart_shift(3)
```

### MPI_Cart_sub.md
```
MPI_Cart_sub(3)                       MPI                      MPI_Cart_sub(3)



NAME
       MPI_Cart_sub  -   Partitions  a communicator into subgroups which  form
       lower-dimensional cartesian subgrids

SYNOPSIS
       #include "mpi.h"
       int MPI_Cart_sub ( MPI_Comm comm, int *remain_dims, MPI_Comm *comm_new )

INPUT PARAMETERS
       comm   - communicator with cartesian structure (handle)
       remain_dims
              - the i th entry of  remain_dims  specifies  whether  the  i  th
              dimension  is  kept  in the subgrid (true) or is dropped (false)
              (logical vector)


OUTPUT PARAMETER
       newcomm
              - communicator containing the subgrid that includes the  calling
              process (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       cart_sub.c



                                  11/14/2001                   MPI_Cart_sub(3)
```

### MPI_Comm_compare.md
```
MPI_Comm_compare(3)                   MPI                  MPI_Comm_compare(3)



NAME
       MPI_Comm_compare -  Compares two communicators

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_compare (
               MPI_Comm  comm1,
               MPI_Comm  comm2,
               int *result)

INPUT PARAMETERS
       comm1  - comm1 (handle)
       comm2  - comm2 (handle)


OUTPUT PARAMETER
       result -  integer which is MPI_IDENT if the contexts and groups are the
              same, MPI_CONGRUENT if different contexts but identical  groups,
              MPI_SIMILAR  if  different  contexts  but  similar  groups,  and
              MPI_UNEQUAL otherwise


USING 'MPI_COMM_NULL' WITH 'MPI_COMM_COMPARE'
       It is an error  to  use  MPI_COMM_NULL  as  one  of  the  arguments  to
       MPI_Comm_compare .  The relevant sections of the MPI standard are

       .   (2.4.1  Opaque  Objects)  A null handle argument is an erroneous IN
       argument in MPI calls, unless an exception is explicitly stated in  the
       text that defines the function.

       .   (5.4.1. Communicator Accessors) <no text in MPI_COMM_COMPARE allow-
       ing a null handle>


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       commcompare.c



                                  11/14/2001               MPI_Comm_compare(3)
```

### MPI_Comm_create.md
```
MPI_Comm_create(3)                    MPI                   MPI_Comm_create(3)



NAME
       MPI_Comm_create -  Creates a new communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_create ( MPI_Comm comm, MPI_Group group, MPI_Comm *comm_out )

INPUT PARAMETERS
       comm   - communicator (handle)
       group  - group, which is a subset of the group of comm (handle)


OUTPUT PARAMETER
       comm_out
              - new communicator (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Comm_free

LOCATION
       comm_create.c



                                  11/14/2001                MPI_Comm_create(3)
```

### MPI_Comm_dup.md
```
MPI_Comm_dup(3)                       MPI                      MPI_Comm_dup(3)



NAME
       MPI_Comm_dup -  Duplicates an existing communicator with all its cached
       information

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_dup (
               MPI_Comm comm,
               MPI_Comm *comm_out )

INPUT PARAMETER
       comm   - communicator (handle)


OUTPUT PARAMETER
       newcomm
              - A new communicator over the same group as comm but with a  new
              context. See notes.  (handle)


NOTES
       This routine is used to create a new communicator that has a new commu-
       nication context but contains the same group of processes as the  input
       communicator.  Since all MPI communication is performed within a commu-
       nicator (specifies as the group of processes plus  the  context),  this
       routine  provides an effective way to create a private communicator for
       use by a software module or library.  In particular, no library routine
       should  use MPI_COMM_WORLD as the communicator; instead, a duplicate of
       a user-specified communicator should always be used.  For more informa-
       tion, see Using MPI, 2nd edition.

       Because  this routine essentially produces a copy of a communicator, it
       also copies any attributes that have been defined on the input communi-
       cator, using the attribute copy function specified by the copy_function
       argument to MPI_Keyval_create .  This is particularly  useful  for  (a)
       attributes that describe some property of the group associated with the
       communicator, such as its interconnection topology and  (b)  communica-
       tors  that  are  given back to the user; the attibutes in this case can
       track subsequent MPI_Comm_dup operations on this communicator.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Comm_free, MPI_Keyval_create, MPI_Attr_set, MPI_Attr_delete


LOCATION
       comm_dup.c



                                  11/14/2001                   MPI_Comm_dup(3)
```

### MPI_Comm_free.md
```
MPI_Comm_free(3)                      MPI                     MPI_Comm_free(3)



NAME
       MPI_Comm_free -  Marks the communicator object for deallocation

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_free ( MPI_Comm *commp )

INPUT PARAMETER
       comm   - communicator to be destroyed (handle)


NULL HANDLES
       The MPI 1.1 specification, in the section on opaque objects, explicitly

DISALLOWS FREEING A NULL COMMUNICATOR. THE TEXT FROM THE STANDARD IS
       A null handle argument is an erroneous IN argument in MPI calls, unless an
       exception is explicitly stated in the text that defines the function. Such
       exception is allowed for handles to request objects in Wait and Test calls
       (sections Communication Completion and Multiple Completions ). Otherwise, a
       null handle can only be passed to a function that allocates a new object and
       returns a reference to it in the handle.



NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       comm_free.c



                                  10/31/2002                  MPI_Comm_free(3)
```

### MPI_Comm_group.md
```
MPI_Comm_group(3)                     MPI                    MPI_Comm_group(3)



NAME
       MPI_Comm_group -  Accesses the group associated with given communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_group (
               MPI_Comm comm,
               MPI_Group *group )

INPUT PARAMETER
       comm   - Communicator


OUTPUT PARAMETER
       group  - Group in communicator


USING 'MPI_COMM_NULL' WITH 'MPI_COMM_GROUP'
       It is an error  to  use  MPI_COMM_NULL  as  one  of  the  arguments  to
       MPI_Comm_group .  The relevant sections of the MPI standard are

       .   (2.4.1  Opaque  Objects)  A null handle argument is an erroneous IN
       argument in MPI calls, unless an exception is explicitly stated in  the
       text that defines the function.

       .   (5.3.2.  Group  Constructors) <no text in MPI_COMM_GROUP allowing a
       null handle>

       Previous versions of MPICH allow MPI_COMM_NULL in  this  function.   In
       the interests of promoting portability of applications, we have changed
       the behavior of MPI_Comm_group to detect  this  violation  of  the  MPI
       standard.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).

LOCATION
       comm_group.c



                                  11/14/2001                 MPI_Comm_group(3)
```

### MPI_Comm_rank.md
```
MPI_Comm_rank(3)                      MPI                     MPI_Comm_rank(3)



NAME
       MPI_Comm_rank -  Determines the rank of the calling process in the com-
       municator

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_rank ( MPI_Comm comm, int *rank )

INPUT PARAMETERS
       comm   - communicator (handle)


OUTPUT PARAMETER
       rank   - rank of the calling process in group of comm (integer)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).

LOCATION
       comm_rank.c



                                  11/14/2001                  MPI_Comm_rank(3)
```

### MPI_Comm_remote_group.md
```
MPI_Comm_remote_group(3)              MPI             MPI_Comm_remote_group(3)



NAME
       MPI_Comm_remote_group -  Accesses the remote group associated with  the
       given inter-communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_remote_group ( MPI_Comm comm, MPI_Group *group )

INPUT PARAMETER
       comm   - Communicator (must be intercommunicator)


OUTPUT PARAMETER
       group  - remote group of communicator


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).

LOCATION
       comm_rgroup.c



                                  11/14/2001          MPI_Comm_remote_group(3)
```

### MPI_Comm_remote_size.md
```
MPI_Comm_remote_size(3)               MPI              MPI_Comm_remote_size(3)



NAME
       MPI_Comm_remote_size  -  Determines the size of the remote group  asso-
       ciated with an inter-communictor

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_remote_size ( MPI_Comm comm, int *size )

INPUT PARAMETER
       comm   - communicator (handle)


OUTPUT PARAMETER
       size   - number of processes in the group of comm (integer)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       comm_rsize.c



                                  11/14/2001           MPI_Comm_remote_size(3)
```

### MPI_Comm_size.md
```
MPI_Comm_size(3)                      MPI                     MPI_Comm_size(3)



NAME
       MPI_Comm_size  -   Determines  the  size of the group associated with a
       communictor

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_size ( MPI_Comm comm, int *size )

INPUT PARAMETER
       comm   - communicator (handle)


OUTPUT PARAMETER
       size   - number of processes in the group of comm (integer)


NOTES
       MPI_COMM_NULL is not considered a valid argument to this function.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       comm_size.c



                                  11/14/2001                  MPI_Comm_size(3)
```

### MPI_Comm_split.md
```
MPI_Comm_split(3)                     MPI                    MPI_Comm_split(3)



NAME
       MPI_Comm_split -  Creates new communicators based on colors and keys

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_split ( MPI_Comm comm, int color, int key, MPI_Comm *comm_out )

INPUT PARAMETERS
       comm   - communicator (handle)
       color  - control of subset assignment (nonnegative integer).  Processes
              with the same color are in the same new communicator
       key    - control of rank assigment (integer)


OUTPUT PARAMETER
       newcomm
              - new communicator (handle)


NOTES
       The color must be non-negative or MPI_UNDEFINED .



NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ALGORITHM
       The current algorithm used has quite a few (read: a lot of) inefficien-
       cies that can be removed.  Here is what we do for now

       1) A table is built of colors, and keys (has a next field also).
       2) The tables of all processes are merged using
       MPI_Allreduce
       .
       3) Two contexts are allocated for all the comms to be created.  These
       same two contexts can be used for all created communicators since
       the communicators will not overlap.
       4) If the local process has a color of
       MPI_UNDEFINED
       , it can return
       a
       NULL
       comm.
       5) The table entries that match the local process color are sorted
       by key/rank.
       6) A group is created from the sorted list and a communicator is created
       with this group and the previously allocated contexts.



ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Comm_free

LOCATION
       comm_split.c



                                   8/29/2002                 MPI_Comm_split(3)
```

### MPI_Comm_test_inter.md
```
MPI_Comm_test_inter(3)                MPI               MPI_Comm_test_inter(3)



NAME
       MPI_Comm_test_inter -  Tests to see if a comm is an inter-communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Comm_test_inter ( MPI_Comm comm, int *flag )

INPUT PARAMETER
       comm   - communicator (handle)


OUTPUT PARAMETER
       flag   - (logical)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       comm_testic.c



                                  11/14/2001            MPI_Comm_test_inter(3)
```

### MPI_Dims_create.md
```
MPI_Dims_create(3)                    MPI                   MPI_Dims_create(3)



NAME
       MPI_Dims_create -  Creates a division of processors in a cartesian grid

SYNOPSIS
       #include "mpi.h"
       int MPI_Dims_create(
               int nnodes,
               int ndims,
               int *dims)

INPUT PARAMETERS
       nnodes - number of nodes in a grid (integer)
       ndims  - number of cartesian dimensions (integer)


IN/OUT PARAMETER
       dims   - integer array of size ndims specifying the number of nodes  in
              each dimension


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       dims_create.c



                                   4/24/2002                MPI_Dims_create(3)
```

### MPI_Errhandler_create.md
```
MPI_Errhandler_create(3)              MPI             MPI_Errhandler_create(3)



NAME
       MPI_Errhandler_create -  Creates an MPI-style errorhandler

SYNOPSIS
       #include "mpi.h"
       int MPI_Errhandler_create(
               MPI_Handler_function *function,
               MPI_Errhandler       *errhandler)

INPUT PARAMETER
       function
              - user defined error handling procedure


OUTPUT PARAMETER
       errhandler
              - MPI error handler (handle)


NOTES
       The  MPI  Standard  states  that  an implementation may make the output
       value (errhandler) simply the address of the  function.   However,  the
       action  of  MPI_Errhandler_free  makes  this  impossible,  since  it is
       required to set the value of the argument to MPI_ERRHANDLER_NULL .   In
       addition,  the actual error handler must remain until all communicators
       that use it are freed.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.

LOCATION
       errcreate.c



                                  11/14/2001          MPI_Errhandler_create(3)
```

### MPI_Errhandler_free.md
```
MPI_Errhandler_free(3)                MPI               MPI_Errhandler_free(3)



NAME
       MPI_Errhandler_free -  Frees an MPI-style errorhandler

SYNOPSIS
       #include "mpi.h"
       int MPI_Errhandler_free( MPI_Errhandler *errhandler )

INPUT PARAMETER
       errhandler
              -  MPI  error  handler  (handle).  Set to MPI_ERRHANDLER_NULL on
              exit.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       errfree.c



                                  11/14/2001            MPI_Errhandler_free(3)
```

### MPI_Errhandler_get.md
```
MPI_Errhandler_get(3)                 MPI                MPI_Errhandler_get(3)



NAME
       MPI_Errhandler_get -  Gets the error handler for a communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Errhandler_get( MPI_Comm comm, MPI_Errhandler *errhandler )

INPUT PARAMETER
       comm   - communicator to get the error handler from (handle)


OUTPUT PARAMETER
       errhandler
              - MPI error handler currently associated with communicator (han-
              dle)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


NOTE ON IMPLEMENTATION
       The  MPI Standard was unclear on whether this routine required the user
       to call MPI_Errhandler_free once for each call made to this routine  in
       order  to  free  the  error  handler.  After some debate, the MPI Forum
       added an explicit statement that users are required to call MPI_Errhan-
       dler_free  when the return value from this routine is no longer needed.
       This behavior is similar to the other MPI routines for getting objects;
       for  example, MPI_Comm_group requires that the user call MPI_Group_free
       when the group returned by MPI_Comm_group is no longer needed.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       errget.c



                                  11/14/2001             MPI_Errhandler_get(3)
```

### MPI_Errhandler_set.md
```
MPI_Errhandler_set(3)                 MPI                MPI_Errhandler_set(3)



NAME
       MPI_Errhandler_set -  Sets the error handler for a communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Errhandler_set( MPI_Comm comm, MPI_Errhandler errhandler )

INPUT PARAMETERS
       comm   - communicator to set the error handler for (handle)
       errhandler
              - new MPI error handler for communicator (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       errset.c



                                  11/14/2001             MPI_Errhandler_set(3)
```

### MPI_Error_class.md
```
MPI_Error_class(3)                    MPI                   MPI_Error_class(3)



NAME
       MPI_Error_class -  Converts an error code into an error class

SYNOPSIS
       #include "mpi.h"
       int MPI_Error_class(
               int errorcode,
               int *errorclass)

INPUT PARAMETER
       errorcode
              - Error code returned by an MPI routine


OUTPUT PARAMETER
       errorclass
              - Error class associated with errorcode



NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       errclass.c



                                  11/14/2001                MPI_Error_class(3)
```

### MPI_Error_string.md
```
MPI_Error_string(3)                   MPI                  MPI_Error_string(3)



NAME
       MPI_Error_string -  Return a string for a given error code

SYNOPSIS
       #include "mpi.h"
       int MPI_Error_string( int errorcode, char *string, int *resultlen )

INPUT PARAMETERS
       errorcode
              - Error code returned by an MPI routine or an MPI error class


OUTPUT PARAMETER
       string - Text that corresponds to the errorcode
       resultlen
              - Length of string

              Notes:  Error codes are the values return by MPI routines (in C)
              or in the ierr argument (in Fortran).  These  can  be  converted
              into error classes with the routine MPI_Error_class .



NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       errorstring.c



                                  11/14/2001               MPI_Error_string(3)
```

### MPI_Finalize.md
```
MPI_Finalize(3)                       MPI                      MPI_Finalize(3)



NAME
       MPI_Finalize -  Terminates MPI execution environment

SYNOPSIS
       #include "mpi.h"
       int MPI_Finalize()

NOTES
       All  processes  must  call  this routine before exiting.  The number of
       processes running after this routine is called is undefined; it is best
       not  to perform much more than a return rc after calling MPI_Finalize .



NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       finalize.c



                                   4/9/2002                    MPI_Finalize(3)
```

### MPI_Gather.md
```
MPI_Gather(3)                         MPI                        MPI_Gather(3)



NAME
       MPI_Gather -  Gathers together values from a group of processes

SYNOPSIS
       #include "mpi.h"
       int MPI_Gather ( void *sendbuf, int sendcnt, MPI_Datatype sendtype,
                       void *recvbuf, int recvcount, MPI_Datatype recvtype,
                       int root, MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - starting address of send buffer (choice)
       sendcount
              - number of elements in send buffer (integer)
       sendtype
              - data type of send buffer elements (handle)
       recvcount
              -  number  of elements for any single receive (integer, signifi-
              cant only at root)
       recvtype
              - data type of recv buffer elements (significant only  at  root)
              (handle)
       root   - rank of receiving process (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - address of receive buffer (choice, significant only at root )


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              - Invalid buffer pointer.  Usually a null buffer  where  one  is
              not valid.

LOCATION
       gather.c



                                  11/14/2001                     MPI_Gather(3)
```

### MPI_Gatherv.md
```
MPI_Gatherv(3)                        MPI                       MPI_Gatherv(3)



NAME
       MPI_Gatherv -  Gathers into specified locations from all processes in a
       group

SYNOPSIS
       #include "mpi.h"
       int MPI_Gatherv ( void *sendbuf, int sendcnt, MPI_Datatype sendtype,
                         void *recvbuf, int *recvcnts, int *displs,
                        MPI_Datatype recvtype,
                         int root, MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - starting address of send buffer (choice)
       sendcount
              - number of elements in send buffer (integer)
       sendtype
              - data type of send buffer elements (handle)
       recvcounts
              - integer array (of length group size) containing the number  of
              elements  that  are received from each process (significant only
              at root )
       displs - integer array (of length group size). Entry  i  specifies  the
              displacement relative to recvbuf  at which to place the incoming
              data from process i (significant only at root)
       recvtype
              - data type of recv buffer elements (significant only at root  )
              (handle)
       root   - rank of receiving process (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - address of receive buffer (choice, significant only at root )


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              -  Invalid  buffer  pointer.  Usually a null buffer where one is
              not valid.

LOCATION
       gatherv.c



                                   2/19/2002                    MPI_Gatherv(3)
```

### MPI_Get_count.md
```
MPI_Get_count(3)                      MPI                     MPI_Get_count(3)



NAME
       MPI_Get_count -  Gets the number of "top level" elements

SYNOPSIS
       #include "mpi.h"
       int MPI_Get_count(
               MPI_Status *status,
               MPI_Datatype datatype,
               int *count )

INPUT PARAMETERS
       status - return status of receive operation (Status)
       datatype
              - datatype of each receive buffer element (handle)


OUTPUT PARAMETER
       count  -  number  of  received elements (integer) Notes: If the size of
              the datatype is zero, this routine will return a count of  zero.
              If  the amount of data in status is not an exact multiple of the
              size of datatype (so that count would not be integral), a  count
              of MPI_UNDEFINED is returned instead.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).

LOCATION
       getcount.c



                                  11/14/2001                  MPI_Get_count(3)
```

### MPI_Get_elements.md
```
MPI_Get_elements(3)                   MPI                  MPI_Get_elements(3)



NAME
       MPI_Get_elements -  Returns the number of basic elements in a datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Get_elements ( MPI_Status *status, MPI_Datatype datatype,
                             int *elements )

INPUT PARAMETERS
       status - return status of receive operation (Status)
       datatype
              - datatype used by receive operation (handle)


OUTPUT PARAMETER
       count  - number of received basic elements (integer)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).


LOCATION
       getelements.c



                                  11/14/2001               MPI_Get_elements(3)
```

### MPI_Get_processor_name.md
```
MPI_Get_processor_name(3)             MPI            MPI_Get_processor_name(3)



NAME
       MPI_Get_processor_name -  Gets the name of the processor

SYNOPSIS
       #include "mpi.h"
       int MPI_Get_processor_name(
               char *name,
               int *resultlen)

OUTPUT PARAMETERS
       name   -  A  unique  specifier  for  the actual (as opposed to virtual)
              node. This must be an array of  size  at  least  MPI_MAX_PROCES-
              SOR_NAME .

       resultlen
              - Length (in characters) of the name


NOTES
       The  name  returned should identify a particular piece of hardware; the
       exact format is implementation defined.  This name may or  may  not  be
       the same as might be returned by gethostname , uname , or sysinfo .



NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       getpname.c



                                  11/14/2001         MPI_Get_processor_name(3)
```

### MPI_Get_version.md
```
MPI_Get_version(3)                    MPI                   MPI_Get_version(3)



NAME
       MPI_Get_version -  Gets the version of MPI

SYNOPSIS
       #include "mpi.h"
       int MPI_Get_version(
               int *version,
               int *subversion )

OUTPUT PARAMETERS
       version
              - Major version of MPI (1 or 2)
       subversion
              - Minor version of MPI.


NOTES
       The  defined  values  MPI_VERSION  and  MPI_SUBVERSION contain the same
       information.  This routine allows you to check that the library matches
       the version specified in the mpi.h and mpif.h files.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       getversion.c



                                  11/14/2001                MPI_Get_version(3)

```

### MPI_Graph_create.md
```
MPI_Graph_create(3)                   MPI                  MPI_Graph_create(3)



NAME
       MPI_Graph_create -  Makes a new communicator to which topology informa-
       tion has been attached

SYNOPSIS
       #include "mpi.h"
       int MPI_Graph_create ( MPI_Comm comm_old, int nnodes, int *index, int *edges,
                             int reorder, MPI_Comm *comm_graph )

INPUT PARAMETERS
       comm_old
              - input communicator without topology (handle)
       nnodes - number of nodes in graph (integer)
       index  - array of integers describing node degrees (see below)
       edges  - array of integers describing graph edges (see below)
       reorder
              - ranking may be reordered (true) or not (false) (logical)


OUTPUT PARAMETER
       comm_graph
              - communicator with graph topology added (handle)


ALGORITHM
       We ignore the reorder info currently.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       graphcreate.c



                                   1/4/2002                MPI_Graph_create(3)
```

### MPI_Graphdims_get.md
```
MPI_Graphdims_get(3)                  MPI                 MPI_Graphdims_get(3)



NAME
       MPI_Graphdims_get  -   Retrieves  graph topology information associated
       with a  communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Graphdims_get ( MPI_Comm comm, int *nnodes, int *nedges )

INPUT PARAMETERS
       comm   - communicator for group with graph structure (handle)


OUTPUT PARAMETER
       nnodes - number of nodes in graph (integer)
       nedges - number of edges in graph (integer)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       graphdimsget.c



                                  11/14/2001              MPI_Graphdims_get(3)
```

### MPI_Graph_get.md
```
MPI_Graph_get(3)                      MPI                     MPI_Graph_get(3)



NAME
       MPI_Graph_get -  Retrieves graph topology information associated with a
       communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Graph_get ( MPI_Comm comm, int maxindex, int maxedges,
                          int *index, int *edges )

INPUT PARAMETERS
       comm   - communicator with graph structure (handle)
       maxindex
              - length of vector index in the calling program  (integer)
       maxedges
              - length of vector edges in the calling program  (integer)


OUTPUT PARAMETER
       index  - array of integers containing the graph structure (for  details
              see the definition of MPI_GRAPH_CREATE )
       edges  - array of integers containing the graph structure


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       graph_get.c



                                   1/4/2002                   MPI_Graph_get(3)
```

### MPI_Graph_map.md
```
MPI_Graph_map(3)                      MPI                     MPI_Graph_map(3)



NAME
       MPI_Graph_map -  Maps process to graph topology information

SYNOPSIS
       #include "mpi.h"
       int MPI_Graph_map ( MPI_Comm comm_old, int nnodes, int *index, int *edges,
                          int *newrank )

INPUT PARAMETERS
       comm   - input communicator (handle)
       nnodes - number of graph nodes (integer)
       index  -   integer   array   specifying   the   graph   structure,  see
              MPI_GRAPH_CREATE

       edges  - integer array specifying the graph structure


OUTPUT PARAMETER
       newrank
              - reordered rank of the calling process;  MPI_UNDEFINED  if  the
              calling process does not belong to graph (integer)

NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       graph_map.c



                                   1/4/2002                   MPI_Graph_map(3)
```

### MPI_Graph_neighbors_count.md
```
MPI_Graph_neighbors_count(3)          MPI         MPI_Graph_neighbors_count(3)



NAME
       MPI_Graph_neighbors_count  -  Returns the number of neighbors of a node
       associated with a graph topology

SYNOPSIS
       #include "mpi.h"
       int MPI_Graph_neighbors_count ( MPI_Comm comm, int rank, int *nneighbors )

INPUT PARAMETERS
       comm   - communicator with graph topology (handle)
       rank   - rank of process in group of comm (integer)


OUTPUT PARAMETER
       nneighbors
              - number of neighbors of specified process (integer)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_RANK
              - Invalid source or destination rank.   Ranks  must  be  between
              zero  and  the  size  of  the communicator minus one; ranks in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_SOURCE .


LOCATION
       graphnbrcnt.c



                                  11/14/2001      MPI_Graph_neighbors_count(3)
```

### MPI_Graph_neighbors.md
```
MPI_Graph_neighbors(3)                MPI               MPI_Graph_neighbors(3)



NAME
       MPI_Graph_neighbors -  Returns the neighbors of a node associated  with
       a graph topology

SYNOPSIS
       #include "mpi.h"
       int MPI_Graph_neighbors ( MPI_Comm comm, int rank, int maxneighbors,
                               int *neighbors )

INPUT PARAMETERS
       comm   - communicator with graph topology (handle)
       rank   - rank of process in group of comm (integer)
       maxneighbors
              - size of array neighbors (integer)


OUTPUT PARAMETERS
       neighbors
              - ranks of processes that are  neighbors  to  specified  process
              (array of integer)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TOPOLOGY
              - Invalid topology.  Either there is no topology associated with
              this communicator, or it is not the correct type (e.g., MPI_CART
              when expecting MPI_GRAPH ).
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .


LOCATION
       graph_nbr.c



                                  11/14/2001            MPI_Graph_neighbors(3)
```

### MPI_Group_compare.md
```
MPI_Group_compare(3)                  MPI                 MPI_Group_compare(3)



NAME
       MPI_Group_compare -  Compares two groups

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_compare ( MPI_Group group1, MPI_Group group2, int *result )

INPUT PARAMETERS
       group1 - group1 (handle)
       group2 - group2 (handle)


OUTPUT PARAMETER
       result - integer which is MPI_IDENT if the order and members of the two
              groups are the same, MPI_SIMILAR if only  the  members  are  the
              same, and MPI_UNEQUAL otherwise


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       groupcompare.c



                                  11/14/2001              MPI_Group_compare(3)
```

### MPI_Group_difference.md
```
MPI_Group_difference(3)               MPI              MPI_Group_difference(3)



NAME
       MPI_Group_difference -  Makes a group from the difference of two groups

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_difference ( MPI_Group group1, MPI_Group group2,
                                MPI_Group *group_out )

INPUT PARAMETERS
       group1 - first group (handle)
       group2 - second group (handle)


OUTPUT PARAMETER
       newgroup
              - difference group (handle)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Group_free

LOCATION
       group_diff.c



                                  11/14/2001           MPI_Group_difference(3)
```

### MPI_Group_excl.md
```
MPI_Group_excl(3)                     MPI                    MPI_Group_excl(3)



NAME
       MPI_Group_excl  -  Produces a group by reordering an existing group and
       taking only unlisted members

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_excl ( MPI_Group group, int n, int *ranks, MPI_Group *newgroup )

INPUT PARAMETERS
       group  - group (handle)
       n      - number of elements in array ranks (integer)
       ranks  - array of integer ranks in group not to appear in newgroup



OUTPUT PARAMETER
       newgroup
              - new group derived from above, preserving the order defined  by
              group (handle)


NOTE
       Currently,  each  of  the  ranks to exclude must be a valid rank in the
       group and all elements must be distinct or the function  is  erroneous.
       This restriction is per the draft.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .



SEE ALSO
       MPI_Group_free

LOCATION
       group_excl.c



                                  11/14/2001                 MPI_Group_excl(3)
```

### MPI_Group_free.md
```
MPI_Group_free(3)                     MPI                    MPI_Group_free(3)



NAME
       MPI_Group_free -  Frees a group

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_free ( MPI_Group *group )
       Input Parameter
       group  - group (handle)


NOTES
       On output, group is set to MPI_GROUP_NULL .



NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_ARG
              - This error class is associated with an error code  that  indi-
              cates  that  an  attempt  was  made to free one of the permanent
              groups.

LOCATION
       group_free.c



                                  11/14/2001                 MPI_Group_free(3)
```

### MPI_Group_incl.md
```
MPI_Group_incl(3)                     MPI                    MPI_Group_incl(3)



NAME
       MPI_Group_incl  -  Produces a group by reordering an existing group and
       taking only listed members

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_incl ( MPI_Group group, int n, int *ranks, MPI_Group *group_out )

INPUT PARAMETERS
       group  - group (handle)
       n      - number of elements in array ranks  (and  size  of  newgroup  )
              (integer)
       ranks  -  ranks  of  processes in group to appear in newgroup (array of
              integers)


OUTPUT PARAMETER
       newgroup
              - new group derived from above, in the order defined by ranks

              (handle)


NOTE
       This implementation does not currently check to see that  the  list  of
       ranks to ensure that there are no duplicates.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .



SEE ALSO
       MPI_Group_free

LOCATION
       group_incl.c



                                  11/14/2001                 MPI_Group_incl(3)
```

### MPI_Group_intersection.md
```
MPI_Group_intersection(3)             MPI            MPI_Group_intersection(3)



NAME
       MPI_Group_intersection  -   Produces a group as the intersection of two
       existing groups

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_intersection ( MPI_Group group1, MPI_Group group2,
                                  MPI_Group *group_out )

INPUT PARAMETERS
       group1 - first group (handle)
       group2 - second group (handle)


OUTPUT PARAMETER
       newgroup
              - intersection group (handle)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Group_free

LOCATION
       group_inter.c



                                  11/14/2001         MPI_Group_intersection(3)
```

### MPI_Group_range_excl.md
```
MPI_Group_range_excl(3)               MPI              MPI_Group_range_excl(3)



NAME
       MPI_Group_range_excl  -   Produces  a group by excluding ranges of pro-
       cesses from an existing group

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_range_excl ( MPI_Group group, int n, int ranges[][3],
                                MPI_Group *newgroup )

INPUT PARAMETERS
       group  - group (handle)
       n      - number of elements in array ranks (integer)
       ranges - a one-dimensional array of integer triplets of the form (first
              rank,  last rank, stride), indicating the ranks in group of pro-
              cesses to be excluded from the output group newgroup .



OUTPUT PARAMETER
       newgroup
              - new group derived from above, preserving the  order  in  group
              (handle)


NOTE
       Currently,  each  of  the  ranks to exclude must be a valid rank in the
       group and all elements must be distinct or the function  is  erroneous.
       This restriction is per the draft.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.
       MPI_ERR_RANK
              - Invalid source or destination rank.   Ranks  must  be  between
              zero  and  the  size  of  the communicator minus one; ranks in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_SOURCE .

       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).


SEE ALSO
       MPI_Group_free

LOCATION
       group_rexcl.c



                                  11/14/2001           MPI_Group_range_excl(3)
```

### MPI_Group_range_incl.md
```
MPI_Group_range_incl(3)               MPI              MPI_Group_range_incl(3)



NAME
       MPI_Group_range_incl  -  Creates a new group from ranges of ranks in an
       existing group

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_range_incl ( MPI_Group group, int n, int ranges[][3],
                                MPI_Group *newgroup )

INPUT PARAMETERS
       group  - group (handle)
       n      - number of triplets in array ranges (integer)
       ranges - a one-dimensional array  of  integer  triplets,  of  the  form
              (first  rank,  last  rank,  stride) indicating ranks in group or
              processes to be included in newgroup



OUTPUT PARAMETER
       newgroup
              - new group derived from above, in the order defined  by  ranges
              (handle)


NOTE
       This  implementation  does  not currently check to see that the list of
       ranges to include are valid ranks in the group.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_RANK
              - Invalid source or destination rank.   Ranks  must  be  between
              zero  and  the  size  of  the communicator minus one; ranks in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_SOURCE .



SEE ALSO
       MPI_Group_free

LOCATION
       group_rincl.c



                                  11/14/2001           MPI_Group_range_incl(3)
```

### MPI_Group_rank.md
```
MPI_Group_rank(3)                     MPI                    MPI_Group_rank(3)



NAME
       MPI_Group_rank -  Returns the rank of this process in the given group

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_rank ( MPI_Group group, int *rank )

INPUT PARAMETERS
       group  - group (handle)


OUTPUT PARAMETER
       rank   -  rank of the calling process in group, or MPI_UNDEFINED if the
              process is not a member (integer)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).


LOCATION
       group_rank.c



                                  11/14/2001                 MPI_Group_rank(3)
```

### MPI_Group_size.md
```
MPI_Group_size(3)                     MPI                    MPI_Group_size(3)



NAME
       MPI_Group_size -  Returns the size of a group

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_size ( MPI_Group group, int *size )

INPUT PARAMETERS
       group  - group (handle) Output Parameter:
       size   - number of processes in the group (integer)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).


LOCATION
       group_size.c



                                  11/14/2001                 MPI_Group_size(3)
```

### MPI_Group_translate_ranks.md
```
MPI_Group_translate_ranks(3)          MPI         MPI_Group_translate_ranks(3)



NAME
       MPI_Group_translate_ranks  -   Translates the ranks of processes in one
       group to  those in another group

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_translate_ranks ( MPI_Group group_a, int n, int *ranks_a,
                                    MPI_Group group_b, int *ranks_b )

INPUT PARAMETERS
       group1 - group1 (handle)
       n      - number of ranks in ranks1 and ranks2 arrays (integer)
       ranks1 - array of zero or more valid ranks in group1

       group2 - group2 (handle)


OUTPUT PARAMETER
       ranks2 - array of corresponding ranks in group2, MPI_UNDEFINED when  no
              correspondence exists.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_RANK
              - Invalid source or destination rank.   Ranks  must  be  between
              zero  and  the  size  of  the communicator minus one; ranks in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_SOURCE .



LOCATION
       group_tranks.c



                                  11/14/2001      MPI_Group_translate_ranks(3)
```

### MPI_Group_union.md
```
MPI_Group_union(3)                    MPI                   MPI_Group_union(3)



NAME
       MPI_Group_union -  Produces a group by combining two groups

SYNOPSIS
       #include "mpi.h"
       int MPI_Group_union ( MPI_Group group1, MPI_Group group2,
                            MPI_Group *group_out )

INPUT PARAMETERS
       group1 - first group (handle)
       group2 - second group (handle)


OUTPUT PARAMETER
       newgroup
              - union group (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_GROUP
              - Null group passed to function.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Group_free

LOCATION
       group_union.c



                                  11/14/2001                MPI_Group_union(3)
```

### MPI_Ibsend.md
```
MPI_Ibsend(3)                         MPI                        MPI_Ibsend(3)



NAME
       MPI_Ibsend -  Starts a nonblocking buffered send

SYNOPSIS
       #include "mpi.h"
       int MPI_Ibsend( void *buf, int count, MPI_Datatype datatype, int dest, int tag,
                      MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements in send buffer (integer)
       datatype
              - datatype of each send buffer element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_BUFFER
              - Invalid buffer pointer.  Usually a null buffer  where  one  is
              not valid.


LOCATION
       ibsend.c



                                  11/14/2001                     MPI_Ibsend(3)
```

### MPI_Initialized.md
```
MPI_Initialized(3)                    MPI                   MPI_Initialized(3)



NAME
       MPI_Initialized -  Indicates whether MPI_Init has been called.

SYNOPSIS
       #include "mpi.h"
       int MPI_Initialized( int *flag )

OUTPUT PARAMETER
       flag   -  Flag is true if MPI_Init has been called and false otherwise.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       initialize.c



                                  11/14/2001                MPI_Initialized(3)
```

### MPI_Init.md
```
MPI_Init(3)                           MPI                          MPI_Init(3)



NAME
       MPI_Init -  Initialize the MPI execution environment

SYNOPSIS
       #include "mpi.h"
       int MPI_Init(int *argc, char ***argv)

INPUT PARAMETERS
       argc   - Pointer to the number of arguments
       argv   - Pointer to the argument vector


COMMAND LINE ARGUMENTS
       MPI specifies no command-line arguments but does allow an MPI implemen-
       tation to make use of them.

       -mpiqueue
              - print out the state of the message queues when MPI_FINALIZE is
              called.   All  processors print; the output may be hard to deci-
              pher.  This is intended as a debugging aid.

       -mpiversion
              - print out the version of the implementation  (  not  of  MPI),
              including the arguments that were used with configure.

       -mpinice nn
              -  Increments the nice value by nn (lowering the priority of the
              program by nn ).  nn must be positive (except  for  root).   Not
              all systems support this argument; those that do not will ignore
              it.

       -mpedbg
              - Start a debugger in an xterm  window  if  there  is  an  error
              (either detected by MPI or a normally fatal signal).  This works
              only if MPICH was configured with -mpedbg .  CURRENTLY DISABLED.
              If  you  have  TotalView, -mpichtv or mpirun -tv will give you a
              better environment anyway.

       -mpimem
              - If MPICH was built with -DMPIR_DEBUG_MEM  ,  this  checks  all
              malloc  and  free  operations  (internal  to MPICH) for signs of
              injury to the memory allocation areas.

       -mpidb options
              - Activate various debugging options.  Some require  that  MPICH
              have  been  built  with special options.  These are intended for
              debugging MPICH, not for debugging user programs.  The available
              options include:
              mem     - Enable dynamic memory tracing of internal MPI objects
              memall  - Generate output of all memory allocation/deallocation
              ptr     - Enable tracing of internal MPI pointer conversions
              rank n  - Limit subsequent -mpidb options to on the process with
              the specified rank in MPI_COMM_WORLD.  A rank of -1
              selects all of MPI_COMM_WORLD.
              ref     - Trace use of internal MPI objects
              reffile filename - Trace use of internal MPI objects with output
              to the indicated file
              trace   - Trace routine calls



NOTES
       Note  that  the  Fortran  binding  for  this routine has only the error
       return argument ( MPI_INIT(ierror) )

       Because the Fortran and C versions of MPI_Init are different, there  is
       a  restriction  on  who can call MPI_Init .  The version (Fortran or C)
       must match the main program.  That is, if the main  program  is  in  C,
       then  the C version of MPI_Init must be called.  If the main program is
       in Fortran, the Fortran version must be called.

       On exit from this routine, all processes will have a copy of the  argu-
       ment  list.   This  is  not  required  by  the MPI standard, and truely
       portable codes should not rely on it.  This is provided as a service by
       this implementation (an MPI implementation is allowed to distribute the
       command line arguments but is not required to).

       Command line arguments are not provided to Fortran programs.  More pre-
       cisely,  non-standard  Fortran  routines  such as getarg and iargc have
       undefined behavior in MPI and in this implementation.

       The MPI standard does not say what a program can do before an  MPI_INIT
       or  after an MPI_FINALIZE .  In the MPICH implementation, you should do
       as little as possible.  In particular, avoid anything that changes  the
       external  state of the program, such as opening files, reading standard
       input or writing to standard output.


SIGNALS USED
       The MPI standard requires that all signals  used  be  documented.   The
       MPICH  implementation  itself uses no signals, but some of the software
       that MPICH relies on may use some signals.  The list below  is  partial
       and  should  be  independantly checked if you (and any package that you
       use) depend on particular signals.


IBM POE/MPL FOR SP2
       SIGHUP, SIGINT, SIGQUIT, SIGFPE, SIGSEGV,  SIGPIPE,  SIGALRM,  SIGTERM,
       SIGIO


-MPEDBG SWITCH
       SIGQUIT, SIGILL, SIGFPE, SIGBUS, SIGSEGV, SIGSYS


MEIKO CS2
       SIGUSR2


CH_P4 DEVICE
       SIGUSR1

       The ch_p4 device also catches SIGINT, SIGFPE, SIGBUS, and SIGSEGV; this
       helps the p4 device (and MPICH) more gracefully abort a failed program.


INTEL PARAGON (CH_NX AND NX DEVICE)
       SIGUSR2


SHARED MEMORY (CH_SHMEM DEVICE)
       SIGCHLD

       Note  that  if  you are using software that needs the same signals, you
       may find that there is no way to use that software with the MPI  imple-
       mentation.   The  signals  that cause the most trouble for applications
       include SIGIO , SIGALRM , and SIGPIPE .  For example, using  SIGIO  and
       SIGPIPE may prevent X11 routines from working.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_OTHER
              - This error class is associated with an error code  that  indi-
              cates  that  an attempt was made to call MPI_INIT a second time.
              MPI_INIT may only be called once in a program.

LOCATION
       init.c



                                   4/8/2002                        MPI_Init(3)
```

### mpi_init_thread.md
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
<title>404 Not Found</title>
</head>

<body>
<p><strong>HTTP 404 - Not Found</strong><p />

The requested URL was not found on this server.
</body>
</html>
```

### MPI_Intercomm_create.md
```
MPI_Intercomm_create(3)               MPI              MPI_Intercomm_create(3)



NAME
       MPI_Intercomm_create  -  Creates an intercommuncator from two intracom-
       municators

SYNOPSIS
       #include "mpi.h"
       int MPI_Intercomm_create ( MPI_Comm local_comm, int local_leader,
                                MPI_Comm peer_comm, int remote_leader, int tag,
                                MPI_Comm *comm_out )

INPUT PARAMTERS
       local_comm
              - Local (intra)communicator
       local_leader
              - Rank in local_comm of leader (often 0)
       peer_comm
              - Remote communicator
       remote_leader
              - Rank in peer_comm of remote leader (often 0)
       tag    - Message tag to use in constructing intercommunicator; if  mul-
              tiple MPI_Intercomm_creates are being made, they should use dif-
              ferent tags (more precisely, ensure that the  local  and  remote
              leaders  are  using different tags for each MPI_intercomm_create
              ).


OUTPUT PARAMETER
       comm_out
              - Created intercommunicator


NOTES
       The MPI 1.1 Standard contains two mutually exclusive  comments  on  the
       input intracommunicators.  One says that their repective groups must be
       disjoint; the other that the leaders can be the  same  process.   After
       some  discussion  by the MPI Forum, it has been decided that the groups
       must be disjoint.  Note that the reason given for this in the  standard
       is  not  the  reason  for  this choice; rather, the other operations on
       intercommunicators (like MPI_Intercomm_merge ) do not make sense if the
       groups are not disjoint.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ALGORITHM
       1) Allocate a send context, an inter
              - coll context, and an intra-coll context
       2) Send send_context and lrank_to_grank list from local comm group
              - if I'm the local_leader.
       3) If I'm the local leader, then wait on the posted sends and receives
              - to complete.  Post the receive for the remote  group  informa-
              tion and wait for it to complete.
       4) Broadcast information received from the remote leader.
              - . 5) Create the inter_communicator from the information we now
              have.
       An inter
              - communicator ends up with three levels of communicators.   The
              inter-communicator  returned  to the user, a "collective" inter-
              communicator that can be used for  safe  communications  between
              local  & remote groups, and a collective intra-communicator that
              can be used to allocate new contexts during the  merge  and  dup
              operations.

              For the resulting inter-communicator, comm_out


              comm_out                       = inter-communicator
              comm_out->comm_coll            = "collective" inter-communicator
              comm_out->comm_coll->comm_coll = safe collective intra-communicator



ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_TAG
              -  Invalid  tag  argument.  Tags must be non-negative; tags in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .



SEE ALSO
       MPI_Intercomm_merge, MPI_Comm_free, MPI_Comm_remote_group,
       MPI_Comm_remote_size

LOCATION
       ic_create.c



                                  11/14/2001           MPI_Intercomm_create(3)
```

### MPI_Intercomm_merge.md
```
MPI_Intercomm_merge(3)                MPI               MPI_Intercomm_merge(3)



NAME
       MPI_Intercomm_merge  -  Creates an intracommuncator from an intercommu-
       nicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Intercomm_merge ( MPI_Comm comm, int high, MPI_Comm *comm_out )

INPUT PARAMETERS
       comm   - Intercommunicator
       high   - Used to order the groups of the two intracommunicators  within
              comm when creating the new communicator.


OUTPUT PARAMETER
       comm_out
              - Created intracommunicator


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ALGORITHM
       1) Allocate two contexts
       2) Local and remote group leaders swap high values
       3) Determine the high value.
       4) Merge the two groups and make the intra-communicator



ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Intercomm_create, MPI_Comm_free

LOCATION
       ic_merge.c



                                  11/14/2001            MPI_Intercomm_merge(3)
```

### MPI_Iprobe.md
```
MPI_Iprobe(3)                         MPI                        MPI_Iprobe(3)



NAME
       MPI_Iprobe -  Nonblocking test for a message

SYNOPSIS
       #include "mpi.h"
       int MPI_Iprobe( int source, int tag, MPI_Comm comm, int *flag,
                      MPI_Status *status )

INPUT PARAMETERS
       source - source rank, or MPI_ANY_SOURCE (integer)
       tag    - tag value or MPI_ANY_TAG (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       flag   - (logical)
       status - status object (Status)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .



LOCATION
       iprobe.c



                                   12/7/2004                     MPI_Iprobe(3)
```

### MPI_Irecv.md
```
MPI_Irecv(3)                          MPI                         MPI_Irecv(3)



NAME
       MPI_Irecv -  Begins a nonblocking receive

SYNOPSIS
       #include "mpi.h"
       int MPI_Irecv( void *buf, int count, MPI_Datatype datatype, int source,
                      int tag, MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of receive buffer (choice)
       count  - number of elements in receive buffer (integer)
       datatype
              - datatype of each receive buffer element (handle)
       source - rank of source (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       irecv.c



                                  11/14/2001                      MPI_Irecv(3)
```

### MPI_Irsend.md
```
MPI_Irsend(3)                         MPI                        MPI_Irsend(3)



NAME
       MPI_Irsend -  Starts a nonblocking ready send

SYNOPSIS
       #include "mpi.h"
       int MPI_Irsend( void *buf, int count, MPI_Datatype datatype, int dest,
                      int tag, MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements in send buffer (integer)
       datatype
              - datatype of each send buffer element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle) Output Parameter:
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


LOCATION
       irsend.c



                                  11/14/2001                     MPI_Irsend(3)
```

### MPI_Isend.md
```
MPI_Isend(3)                          MPI                         MPI_Isend(3)



NAME
       MPI_Isend -  Begins a nonblocking send

SYNOPSIS
       #include "mpi.h"
       int MPI_Isend( void *buf, int count, MPI_Datatype datatype, int dest, int tag,
                      MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements in send buffer (integer)
       datatype
              - datatype of each send buffer element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


LOCATION
       isend.c



                                  11/14/2001                      MPI_Isend(3)
```

### MPI_Issend.md
```
MPI_Issend(3)                         MPI                        MPI_Issend(3)



NAME
       MPI_Issend -  Starts a nonblocking synchronous send

SYNOPSIS
       #include "mpi.h"
       int MPI_Issend( void *buf, int count, MPI_Datatype datatype, int dest,
                      int tag, MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements in send buffer (integer)
       datatype
              - datatype of each send buffer element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.

LOCATION
       issend.c



                                  11/14/2001                     MPI_Issend(3)
```

### MPI_Keyval_create.md
```
MPI_Keyval_create(3)                  MPI                 MPI_Keyval_create(3)



NAME
       MPI_Keyval_create -  Generates a new attribute key

SYNOPSIS
       #include "mpi.h"
       int MPI_Keyval_create (
               MPI_Copy_function *copy_fn,
               MPI_Delete_function *delete_fn,
               int *keyval,
               void *extra_state )

INPUT PARAMETERS
       copy_fn
              - Copy callback function for keyval

       delete_fn
              - Delete callback function for keyval

       extra_state
              - Extra state for callback functions


OUTPUT PARAMETER
       keyval - key value for future access (integer)


NOTES
       Key values are global (available for any and all communicators).

       There  are  subtle  differences between C and Fortran that require that
       the copy_fn be written in the same language that  MPI_Keyval_create  is
       called  from.   This  should not be a problem for most users; only pro-
       gramers using both Fortran and C in the same program need  to  be  sure
       that they follow this rule.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       keyvalcreate.c



                                  11/14/2001              MPI_Keyval_create(3)
```

### MPI_Keyval_free.md
```
MPI_Keyval_free(3)                    MPI                   MPI_Keyval_free(3)



NAME
       MPI_Keyval_free -  Frees attribute key for communicator cache attribute

SYNOPSIS
       #include "mpi.h"
       int MPI_Keyval_free ( int *keyval )

INPUT PARAMETER
       keyval - Frees the integer key value (integer)


NOTE
       Key values are global (they can be used with any and all communicators)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_ARG
              - This error class is associated with an error code  that  indi-
              cates  that  an  attempt  was  made to free one of the permanent
              keys.


SEE ALSO
       MPI_Keyval_create

LOCATION
       keyval_free.c



                                   6/12/2002                MPI_Keyval_free(3)
```

### MPI_Op_create.md
```
MPI_Op_create(3)                      MPI                     MPI_Op_create(3)



NAME
       MPI_Op_create -  Creates a user-defined combination function handle

SYNOPSIS
       #include "mpi.h"
       int MPI_Op_create(
               MPI_User_function *function,
               int commute,
               MPI_Op *op )

INPUT PARAMETERS
       function
              - user defined function (function)
       commute
              - true if commutative;  false otherwise.


OUTPUT PARAMETER
       op     - operation (handle)


NOTES ON THE USER FUNCTION
       The calling list for the user function type is
       typedef void (MPI_User_function) ( void * a,
       void * b, int * len, MPI_Datatype * );

       where  the  operation  is  b[i] = a[i] op b[i] , for i=0,...,len-1 .  A
       pointer to the datatype given to the MPI collective computation routine
       (i.e.,  MPI_Reduce , MPI_Allreduce , MPI_Scan , or MPI_Reduce_scatter )
       is also passed to the user-specified routine.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


NOTES ON COLLECTIVE OPERATIONS
       The  reduction functions ( MPI_Op ) do not return an error value.  As a
       result, if the functions detect an error, all they  can  do  is  either
       call  MPI_Abort  or silently skip the problem.  Thus, if you change the
       error handler from MPI_ERRORS_ARE_FATAL to something else, for example,
       MPI_ERRORS_RETURN , then no error may be indicated.

       The  reason  for  this is the performance problems in ensuring that all
       collective routines return the same error value.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Op_free

LOCATION
       opcreate.c



                                  11/14/2001                  MPI_Op_create(3)
```

### MPI_Op_free.md
```
MPI_Op_free(3)                        MPI                       MPI_Op_free(3)



NAME
       MPI_Op_free -  Frees a user-defined combination function handle

SYNOPSIS
       #include "mpi.h"
       int MPI_Op_free( MPI_Op *op )

INPUT PARAMETER
       op     - operation (handle)


NOTES
       op is set to MPI_OP_NULL on exit.


NULL HANDLES
       The MPI 1.1 specification, in the section on opaque objects, explicitly

DISALLOWS FREEING A NULL COMMUNICATOR. THE TEXT FROM THE STANDARD IS
       A null handle argument is an erroneous IN argument in MPI calls, unless an
       exception is explicitly stated in the text that defines the function. Such
       exception is allowed for handles to request objects in Wait and Test calls
       (sections Communication Completion and Multiple Completions ). Otherwise, a
       null handle can only be passed to a function that allocates a new object and
       returns a reference to it in the handle.



NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_ARG
              -  Invalid  argument;  the error code associated with this error
              indicates an attempt to free an MPI permanent  operation  (e.g.,
              MPI_SUM ).  *N/ /*N MPI_ERR_PERM_KEY
       MPI_ERR_ARG
              -  Invalid  argument;  the error code associated with this error
              indicates an attempt to free or chnage an MPI  permanent  keyval
              (e.g., MPI_TAG_UB ).  *N/ /*N MPI_ERR_UNKNOWN
       MPI_ERR_UNKNOWN
              -  Unknown error.  You should never see this.  If you do, report
              it to mpi-bugs@mcs.anl.gov .



SEE ALSO
       MPI_Op_create

LOCATION
       opfree.c



                                  11/14/2001                    MPI_Op_free(3)
```

### MPI_Pack.md
```
MPI_Pack(3)                           MPI                          MPI_Pack(3)



NAME
       MPI_Pack -  Packs a datatype into contiguous memory

SYNOPSIS
       #include "mpi.h"
       int MPI_Pack ( void *inbuf, int incount, MPI_Datatype datatype,
                      void *outbuf, int outcount, int *position, MPI_Comm comm )

INPUT PARAMETERS
       inbuf  - input buffer start (choice)
       incount
              - number of input data items (integer)
       datatype
              - datatype of each input data item (handle)
       outcount
              - output buffer size, in bytes (integer)
       position
              - current position in buffer, in bytes (integer)
       comm   - communicator for packed message (handle)


OUTPUT PARAMETER
       outbuf - output buffer start (choice)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).


SEE ALSO
       MPI_Unpack, MPI_Pack_size


LOCATION
       pack.c



                                  11/14/2001                       MPI_Pack(3)
```

### MPI_Pack_size.md
```
MPI_Pack_size(3)                      MPI                     MPI_Pack_size(3)



NAME
       MPI_Pack_size  -  Returns the upper bound on the amount of space needed
       to pack a message

SYNOPSIS
       #include "mpi.h"
       int MPI_Pack_size ( int incount, MPI_Datatype datatype, MPI_Comm comm,
                          int *size )

INPUT PARAMETERS
       incount
              - count argument to packing call (integer)
       datatype
              - datatype argument to packing call (handle)
       comm   - communicator argument to packing call (handle)


OUTPUT PARAMETER
       size   - upper bound on size of packed message, in bytes (integer)


NOTES
       The MPI standard document describes this in terms of MPI_Pack , but  it
       applies  to  both MPI_Pack and MPI_Unpack .  That is, the value size is
       the maximum that is needed by either MPI_Pack or MPI_Unpack .



NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).


LOCATION
       pack_size.c



                                  11/14/2001                  MPI_Pack_size(3)
```

### MPI_Pcontrol.md
```
MPI_Pcontrol(3)                       MPI                      MPI_Pcontrol(3)



NAME
       MPI_Pcontrol -  Controls profiling

SYNOPSIS
       #include "mpi.h"
       int MPI_Pcontrol( int level )

INPUT PARAMETERS
       level  - Profiling level


NOTES
       This  routine  provides  a common interface for profiling control.  The
       interpretation of level and any other arguments is left to the  profil-
       ing library.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       pcontrol.c



                                  11/14/2001                   MPI_Pcontrol(3)
```

### MPI_Probe.md
```
MPI_Probe(3)                          MPI                         MPI_Probe(3)



NAME
       MPI_Probe -  Blocking test for a message

SYNOPSIS
       #include "mpi.h"
       int MPI_Probe( int source, int tag, MPI_Comm comm, MPI_Status *status )

INPUT PARAMETERS
       source - source rank, or MPI_ANY_SOURCE (integer)
       tag    - tag value or MPI_ANY_TAG (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       status - status object (Status)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .


LOCATION
       probe.c



                                   12/7/2004                      MPI_Probe(3)
```

### MPI_Recv_init.md
```
MPI_Recv_init(3)                      MPI                     MPI_Recv_init(3)



NAME
       MPI_Recv_init -  Builds a handle for a receive

SYNOPSIS
       #include "mpi.h"
       int MPI_Recv_init( void *buf, int count, MPI_Datatype datatype, int source,
                         int tag, MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of receive buffer (choice)
       count  - number of elements received (integer)
       datatype
              - type of each element (handle)
       source - rank of source or MPI_ANY_SOURCE (integer)
       tag    - message tag or MPI_ANY_TAG (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Start, MPI_Request_free

LOCATION
       create_recv.c



                                  11/14/2001                  MPI_Recv_init(3)
```

### MPI_Recv.md
```
MPI_Recv(3)                           MPI                          MPI_Recv(3)



NAME
       MPI_Recv -  Basic receive

SYNOPSIS
       #include "mpi.h"
       int MPI_Recv( void *buf, int count, MPI_Datatype datatype, int source,
                     int tag, MPI_Comm comm, MPI_Status *status )

OUTPUT PARAMETERS
       buf    - initial address of receive buffer (choice)
       status - status object (Status)


INPUT PARAMETERS
       count  - maximum number of elements in receive buffer (integer)
       datatype
              - datatype of each receive buffer element (handle)
       source - rank of source (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


NOTES
       The  count  argument  indicates  the  maximum  length of a message; the
       actual number can be determined with MPI_Get_count .



NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TAG
              -  Invalid  tag  argument.  Tags must be non-negative; tags in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              - Invalid source or destination rank.   Ranks  must  be  between
              zero  and  the  size  of  the communicator minus one; ranks in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_SOURCE .



LOCATION
       recv.c



                                   2/24/2004                       MPI_Recv(3)
```

### MPI_Reduce.md
```
MPI_Reduce(3)                         MPI                        MPI_Reduce(3)



NAME
       MPI_Reduce -  Reduces values on all processes to a single value

SYNOPSIS
       #include "mpi.h"
       int MPI_Reduce ( void *sendbuf, void *recvbuf, int count,
                       MPI_Datatype datatype, MPI_Op op, int root, MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - address of send buffer (choice)
       count  - number of elements in send buffer (integer)
       datatype
              - data type of elements of send buffer (handle)
       op     - reduce operation (handle)
       root   - rank of root process (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - address of receive buffer (choice, significant only at root )


ALGORITHM
       This implementation currently uses a simple tree algorithm.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


NOTES ON COLLECTIVE OPERATIONS
       The reduction functions ( MPI_Op ) do not return an error value.  As  a
       result,  if  the  functions  detect an error, all they can do is either
       call MPI_Abort or silently skip the problem.  Thus, if you  change  the
       error handler from MPI_ERRORS_ARE_FATAL to something else, for example,
       MPI_ERRORS_RETURN , then no error may be indicated.

       The reason for this is the performance problems in  ensuring  that  all
       collective routines return the same error value.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              -  Invalid  buffer  pointer.  Usually a null buffer where one is
              not valid.
       MPI_ERR_BUFFER
              - This error class is associcated with an error code that  indi-
              cates  that  two  buffer  arguments  are  aliased ; that is, the
              describe overlapping storage (often  the  exact  same  storage).
              This  is prohibited in MPI (because it is prohibited by the For-
              tran standard, and rather than have a separate case  for  C  and
              Fortran, the MPI Forum adopted the more restrictive requirements
              of Fortran).

LOCATION
       reduce.c



                                   2/19/2002                     MPI_Reduce(3)
```

### MPI_Reduce_scatter.md
```
MPI_Reduce_scatter(3)                 MPI                MPI_Reduce_scatter(3)



NAME
       MPI_Reduce_scatter -  Combines values and scatters the results

SYNOPSIS
       #include "mpi.h"
       int MPI_Reduce_scatter ( void *sendbuf, void *recvbuf, int *recvcnts,
                              MPI_Datatype datatype, MPI_Op op, MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - starting address of send buffer (choice)
       recvcounts
              - integer array specifying the number of elements in result dis-
              tributed to each process.  Array must be identical on all  call-
              ing processes.
       datatype
              - data type of elements of input buffer (handle)
       op     - operation (handle)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - starting address of receive buffer (choice)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


NOTES ON COLLECTIVE OPERATIONS
       The reduction functions ( MPI_Op ) do not return an error value.  As  a
       result,  if  the  functions  detect an error, all they can do is either
       call MPI_Abort or silently skip the problem.  Thus, if you  change  the
       error handler from MPI_ERRORS_ARE_FATAL to something else, for example,
       MPI_ERRORS_RETURN , then no error may be indicated.

       The reason for this is the performance problems in  ensuring  that  all
       collective routines return the same error value.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              -  Invalid  buffer  pointer.  Usually a null buffer where one is
              not valid.
       MPI_ERR_OP
              - Invalid operation.  MPI operations (objects of type  MPI_Op  )
              must either be one of the predefined operations (e.g., MPI_SUM )
              or created with MPI_Op_create .

       MPI_ERR_BUFFER
              - This error class is associcated with an error code that  indi-
              cates  that  two  buffer  arguments  are  aliased ; that is, the
              describe overlapping storage (often  the  exact  same  storage).
              This  is prohibited in MPI (because it is prohibited by the For-
              tran standard, and rather than have a separate case  for  C  and
              Fortran, the MPI Forum adopted the more restrictive requirements
              of Fortran).

LOCATION
       red_scat.c



                                  11/14/2001             MPI_Reduce_scatter(3)
```

### MPI_Request_free.md
```
MPI_Request_free(3)                   MPI                  MPI_Request_free(3)



NAME
       MPI_Request_free -  Frees a communication request object

SYNOPSIS
       #include "mpi.h"
       int MPI_Request_free( MPI_Request *request )

INPUT PARAMETER
       request
              - communication request (handle)


NOTES
       This  routine is normally used to free persistent requests created with
       either MPI_Recv_init or MPI_Send_init and friends.  However, it can  be
       used to free a request created with MPI_Irecv or MPI_Isend and friends;
       in that case the use can not use the test/wait routines on the request.

       It  is  permitted  to free an active request.  However, once freed, you
       can not use the request in a wait or test routine (e.g., MPI_Wait ).


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_REQUEST
              - Invalid MPI_Request .  Either  null  or,  in  the  case  of  a
              MPI_Start or MPI_Startall , not a persistent request.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).


SEE ALSO
       also: MPI_Isend, MPI_Irecv, MPI_Issend, MPI_Ibsend, MPI_Irsend,
       MPI_Recv_init, MPI_Send_init, MPI_Ssend_init, MPI_Rsend_init, MPI_Wait,
       MPI_Test, MPI_Waitall, MPI_Waitany, MPI_Waitsome, MPI_Testall, MPI_Tes-
       tany, MPI_Testsome

LOCATION
       commreq_free.c



                                  11/14/2001               MPI_Request_free(3)
```

### MPI_Rsend_init.md
```
MPI_Rsend_init(3)                     MPI                    MPI_Rsend_init(3)



NAME
       MPI_Rsend_init -  Builds a handle for a ready send

SYNOPSIS
       #include "mpi.h"
       int MPI_Rsend_init( void *buf, int count, MPI_Datatype datatype, int dest,
                          int tag, MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements sent (integer)
       datatype
              - type of each element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Start, MPI_Request_free, MPI_Send_init

LOCATION
       rsend_init.c



                                  11/14/2001                 MPI_Rsend_init(3)
```

### MPI_Rsend.md
```
MPI_Rsend(3)                          MPI                         MPI_Rsend(3)



NAME
       MPI_Rsend -  Basic ready send

SYNOPSIS
       #include "mpi.h"
       int MPI_Rsend( void *buf, int count, MPI_Datatype datatype, int dest,
                      int tag, MPI_Comm comm )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements in send buffer (nonnegative integer)
       datatype
              - datatype of each send buffer element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .



LOCATION
       rsend.c



                                  11/14/2001                      MPI_Rsend(3)
```

### MPI_Scan.md
```
MPI_Scan(3)                           MPI                          MPI_Scan(3)



NAME
       MPI_Scan -  Computes the scan (partial reductions) of data on a collec-
       tion of processes

SYNOPSIS
       #include "mpi.h"
       int MPI_Scan ( void *sendbuf, void *recvbuf, int count, MPI_Datatype datatype,
                      MPI_Op op, MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - starting address of send buffer (choice)
       count  - number of elements in input buffer (integer)
       datatype
              - data type of elements of input buffer (handle)
       op     - operation (handle)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - starting address of receive buffer (choice)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


NOTES ON COLLECTIVE OPERATIONS
       The  reduction functions ( MPI_Op ) do not return an error value.  As a
       result, if the functions detect an error, all they  can  do  is  either
       call  MPI_Abort  or silently skip the problem.  Thus, if you change the
       error handler from MPI_ERRORS_ARE_FATAL to something else, for example,
       MPI_ERRORS_RETURN , then no error may be indicated.

       The  reason  for  this is the performance problems in ensuring that all
       collective routines return the same error value.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              - Invalid buffer pointer.  Usually a null buffer  where  one  is
              not valid.
       MPI_ERR_BUFFER
              -  This error class is associcated with an error code that indi-
              cates that two buffer arguments  are  aliased  ;  that  is,  the
              describe  overlapping  storage  (often  the exact same storage).
              This is prohibited in MPI (because it is prohibited by the  For-
              tran  standard,  and  rather than have a separate case for C and
              Fortran, the MPI Forum adopted the more restrictive requirements
              of Fortran).

LOCATION
       scan.c



                                  11/14/2001                       MPI_Scan(3)
```

### MPI_Scatter.md
```
MPI_Scatter(3)                        MPI                       MPI_Scatter(3)



NAME
       MPI_Scatter -  Sends data from one task to all other tasks in a group

SYNOPSIS
       #include "mpi.h"
       int MPI_Scatter (
               void *sendbuf,
               int sendcnt,
               MPI_Datatype sendtype,
               void *recvbuf,
               int recvcnt,
               MPI_Datatype recvtype,
               int root,
               MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - address of send buffer (choice, significant only at root )
       sendcount
              -  number of elements sent to each process (integer, significant
              only at root )
       sendtype
              - data type of send buffer elements (significant only at root  )
              (handle)
       recvcount
              - number of elements in receive buffer (integer)
       recvtype
              - data type of receive buffer elements (handle)
       root   - rank of sending process (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - address of receive buffer (choice)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              - Invalid buffer pointer.  Usually a null buffer  where  one  is
              not valid.

LOCATION
       scatter.c



                                   4/5/2004                     MPI_Scatter(3)
```

### MPI_Scatterv.md
```
MPI_Scatterv(3)                       MPI                      MPI_Scatterv(3)



NAME
       MPI_Scatterv -  Scatters a buffer in parts to all tasks in a group

SYNOPSIS
       #include "mpi.h"
       int MPI_Scatterv (
               void *sendbuf,
               int *sendcnts,
               int *displs,
               MPI_Datatype sendtype,
               void *recvbuf,
               int recvcnt,
               MPI_Datatype recvtype,
               int root,
               MPI_Comm comm )

INPUT PARAMETERS
       sendbuf
              - address of send buffer (choice, significant only at root )
       sendcounts
              -  integer array (of length group size) specifying the number of
              elements to send to each processor
       displs - integer array (of length group size). Entry  i  specifies  the
              displacement (relative to sendbuf  from which to take the outgo-
              ing data to process i

       sendtype
              - data type of send buffer elements (handle)
       recvcount
              - number of elements in receive buffer (integer)
       recvtype
              - data type of receive buffer elements (handle)
       root   - rank of sending process (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       recvbuf
              - address of receive buffer (choice)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_BUFFER
              -  Invalid  buffer  pointer.  Usually a null buffer where one is
              not valid.

LOCATION
       scatterv.c



                                   2/21/2002                   MPI_Scatterv(3)
```

### MPI_Send_init.md
```
MPI_Send_init(3)                      MPI                     MPI_Send_init(3)



NAME
       MPI_Send_init -  Builds a handle for a standard send

SYNOPSIS
       #include "mpi.h"
       int MPI_Send_init( void *buf, int count, MPI_Datatype datatype, int dest,
                         int tag, MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements sent (integer)
       datatype
              - type of each element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle) Output Parameter:
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


SEE ALSO
       MPI_Start, MPI_Startall, MPI_Request_free

LOCATION
       create_send.c



                                  11/14/2001                  MPI_Send_init(3)
```

### MPI_Send.md
```
MPI_Send(3)                           MPI                          MPI_Send(3)



NAME
       MPI_Send -  Performs a basic send

SYNOPSIS
       #include "mpi.h"
       int MPI_Send( void *buf, int count, MPI_Datatype datatype, int dest,
                     int tag, MPI_Comm comm )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements in send buffer (nonnegative integer)
       datatype
              - datatype of each send buffer element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


NOTES
       This routine may block until the message is received.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .



SEE ALSO
       MPI_Isend, MPI_Bsend

LOCATION
       send.c



                                  11/14/2001                       MPI_Send(3)
```

### MPI_Sendrecv.md
```
MPI_Sendrecv(3)                       MPI                      MPI_Sendrecv(3)



NAME
       MPI_Sendrecv -  Sends and receives a message

SYNOPSIS
       #include "mpi.h"
       int MPI_Sendrecv( void *sendbuf, int sendcount, MPI_Datatype sendtype,
                        int dest, int sendtag,
                         void *recvbuf, int recvcount, MPI_Datatype recvtype,
                        int source, int recvtag, MPI_Comm comm, MPI_Status *status )

INPUT PARAMETERS
       sendbuf
              - initial address of send buffer (choice)
       sendcount
              - number of elements in send buffer (integer)
       sendtype
              - type of elements in send buffer (handle)
       dest   - rank of destination (integer)
       sendtag
              - send tag (integer)
       recvcount
              - number of elements in receive buffer (integer)
       recvtype
              - type of elements in receive buffer (handle)
       source - rank of source (integer)
       recvtag
              - receive tag (integer)
       comm   - communicator (handle)


OUTPUT PARAMETERS
       recvbuf
              - initial address of receive buffer (choice)
       status - status object (Status).  This refers to the receive operation.

NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              -  Invalid  tag  argument.  Tags must be non-negative; tags in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              - Invalid source or destination rank.   Ranks  must  be  between
              zero  and  the  size  of  the communicator minus one; ranks in a
              receive ( MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.)  may  also
              be MPI_ANY_SOURCE .



LOCATION
       sendrecv.c



                                  11/14/2001                   MPI_Sendrecv(3)
```

### MPI_Sendrecv_replace.md
```
MPI_Sendrecv_replace(3)               MPI              MPI_Sendrecv_replace(3)



NAME
       MPI_Sendrecv_replace -  Sends and receives using a single buffer

SYNOPSIS
       #include "mpi.h"
       int MPI_Sendrecv_replace( void *buf, int count, MPI_Datatype datatype,
                               int dest, int sendtag, int source, int recvtag,
                               MPI_Comm comm, MPI_Status *status )

INPUT PARAMETERS
       count  - number of elements in send and receive buffer (integer)
       datatype
              - type of elements in send and receive buffer (handle)
       dest   - rank of destination (integer)
       sendtag
              - send message tag (integer)
       source - rank of source (integer)
       recvtag
              - receive message tag (integer)
       comm   - communicator (handle)


OUTPUT PARAMETERS
       buf    - initial address of send and receive buffer (choice)
       status - status object (Status)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .

       MPI_ERR_TRUNCATE
              - Message truncated on receive.  The buffer size  specified  was
              too small for the received message.  This is a recoverable error
              in the MPICH implementation.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.


LOCATION
       sendrecv_rep.c



                                  11/14/2001           MPI_Sendrecv_replace(3)
```

### MPI_Ssend_init.md
```
MPI_Ssend_init(3)                     MPI                    MPI_Ssend_init(3)



NAME
       MPI_Ssend_init -  Builds a handle for a synchronous send

SYNOPSIS
       #include "mpi.h"
       int MPI_Ssend_init( void *buf, int count, MPI_Datatype datatype, int dest,
                          int tag, MPI_Comm comm, MPI_Request *request )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements sent (integer)
       datatype
              - type of each element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


OUTPUT PARAMETER
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .


LOCATION
       ssend_init.c



                                  11/14/2001                 MPI_Ssend_init(3)
```

### MPI_Ssend.md
```
MPI_Ssend(3)                          MPI                         MPI_Ssend(3)



NAME
       MPI_Ssend -  Basic synchronous send

SYNOPSIS
       #include "mpi.h"
       int MPI_Ssend( void *buf, int count, MPI_Datatype datatype,
                      int dest, int tag, MPI_Comm comm )

INPUT PARAMETERS
       buf    - initial address of send buffer (choice)
       count  - number of elements in send buffer (nonnegative integer)
       datatype
              - datatype of each send buffer element (handle)
       dest   - rank of destination (integer)
       tag    - message tag (integer)
       comm   - communicator (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_TAG
              - Invalid tag argument.  Tags must be non-negative;  tags  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_TAG .  The largest tag value is available through the
              the attribute MPI_TAG_UB .

       MPI_ERR_RANK
              -  Invalid  source  or  destination rank.  Ranks must be between
              zero and the size of the communicator  minus  one;  ranks  in  a
              receive  (  MPI_Recv , MPI_Irecv , MPI_Sendrecv , etc.) may also
              be MPI_ANY_SOURCE .


LOCATION
       ssend.c



                                  11/14/2001                      MPI_Ssend(3)
```

### MPI_Startall.md
```
MPI_Startall(3)                       MPI                      MPI_Startall(3)



NAME
       MPI_Startall -  Starts a collection of requests

SYNOPSIS
       #include "mpi.h"
       int MPI_Startall( int count, MPI_Request array_of_requests[] )

INPUT PARAMETERS
       count  - list length (integer)
       array_of_requests
              - array of requests (array of handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       startall.c



                                  11/14/2001                   MPI_Startall(3)
```

### MPI_Start.md
```
MPI_Start(3)                          MPI                         MPI_Start(3)



NAME
       MPI_Start -  Initiates a communication with a persistent request handle

SYNOPSIS
       #include "mpi.h"
       int MPI_Start(
               MPI_Request *request)

INPUT PARAMETER
       request
              - communication request (handle)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_REQUEST
              - Invalid MPI_Request .  Either  null  or,  in  the  case  of  a
              MPI_Start or MPI_Startall , not a persistent request.


LOCATION
       start.c



                                  11/14/2001                      MPI_Start(3)
```

### MPI_Testall.md
```
MPI_Testall(3)                        MPI                       MPI_Testall(3)



NAME
       MPI_Testall  -   Tests  for  the completion of all previously initiated
       communications

SYNOPSIS
       #include "mpi.h"
       int MPI_Testall(
               int count,
               MPI_Request array_of_requests[],
               int *flag,
               MPI_Status array_of_statuses[] )

INPUT PARAMETERS
       count  - lists length (integer)
       array_of_requests
              - array of requests (array of handles)


OUTPUT PARAMETERS
       flag   - (logical)
       array_of_statuses
              - array of status objects (array of Status).   May  be  MPI_STA-
              TUSES_IGNORE .



NOTES
       flag  is  true only if all requests have completed.  Otherwise, flag is
       false and neither the array_of_requests nor  the  array_of_statuses  is
       modified.


NOTE ON STATUS FOR SEND OPERATIONS
       For  send  operations, the only use of status is for MPI_Test_cancelled
       or in the case that there is an error,  in  which  case  the  MPI_ERROR
       field of status will be set.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_IN_STATUS
              -  The  actual  error value is in the MPI_Status argument.  This
              error  class  is  returned  only  from  the  multiple-completion
              routines  ( MPI_Testall , MPI_Testany , MPI_Testsome , MPI_Wait-
              all , MPI_Waitany , and MPI_Waitsome ).  The field MPI_ERROR  in
              the  status argument contains the error value or MPI_SUCCESS (no
              error and complete) or  MPI_ERR_PENDING  to  indicate  that  the
              request  has  not  completed.  The MPI Standard does not specify
              what the result of the multiple completion routines is  when  an
              error occurs.  For example, in an MPI_WAITALL , does the routine
              wait for all requests to either fail or  complete,  or  does  it
              return  immediately  (with  the  MPI  definition of immediately,
              which means independent of  actions  of  other  MPI  processes)?
              MPICH  has  chosen  to  make  the return immediate (alternately,
              local in MPI terms), and to use the error class  MPI_ERR_PENDING
              (introduced in MPI 1.1) to indicate which requests have not com-
              pleted.  In most cases, only one request with an error  will  be
              detected  in  each  call  to  an MPI routine that tests multiple
              requests.  The requests that have not been processed (because an
              error  occured in one of the requests) will have their MPI_ERROR
              field marked with MPI_ERR_PENDING .



LOCATION
       testall.c



                                   2/19/2003                    MPI_Testall(3)
```

### MPI_Testany.md
```
MPI_Testany(3)                        MPI                       MPI_Testany(3)



NAME
       MPI_Testany  -  Tests for completion of any previdously initiated  com-
       munication

SYNOPSIS
       #include "mpi.h"
       int MPI_Testany(
               int count,
               MPI_Request array_of_requests[],
               int *index, int *flag,
               MPI_Status *status )

INPUT PARAMETERS
       count  - list length (integer)
       array_of_requests
              - array of requests (array of handles)


OUTPUT PARAMETERS
       index  - index of operation that completed, or  MPI_UNDEFINED  if  none
              completed (integer)
       flag   - true if one of the operations is complete (logical)
       status - status object (Status).  May be MPI_STATUS_IGNORE .



NOTE ON STATUS FOR SEND OPERATIONS
       For  send  operations, the only use of status is for MPI_Test_cancelled
       or in the case that there is an error,  in  which  case  the  MPI_ERROR
       field of status will be set.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.

LOCATION
       testany.c



                                   1/9/2003                     MPI_Testany(3)
```

### MPI_Test_cancelled.md
```
MPI_Test_cancelled(3)                 MPI                MPI_Test_cancelled(3)



NAME
       MPI_Test_cancelled -  Tests to see if a request was cancelled

SYNOPSIS
       #include "mpi.h"
       int MPI_Test_cancelled(
               MPI_Status *status,
               int        *flag)

INPUT PARAMETER
       status - status object (Status)


OUTPUT PARAMETER
       flag   - (logical)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       testcancel.c



                                  11/14/2001             MPI_Test_cancelled(3)
```

### MPI_Test.md
```
MPI_Test(3)                           MPI                          MPI_Test(3)



NAME
       MPI_Test -  Tests for the completion of a send or receive

SYNOPSIS
       #include "mpi.h"
       int MPI_Test (
               MPI_Request  *request,
               int          *flag,
               MPI_Status   *status)

INPUT PARAMETER
       request
              - communication request (handle)


OUTPUT PARAMETER
       flag   - true if operation completed (logical)
       status - status object (Status).  May be MPI_STATUS_IGNORE .



NOTE ON STATUS FOR SEND OPERATIONS
       For  send  operations, the only use of status is for MPI_Test_cancelled
       or in the case that there is an error,  in  which  case  the  MPI_ERROR
       field of status will be set.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_REQUEST
              -  Invalid  MPI_Request  .   Either  null  or,  in the case of a
              MPI_Start or MPI_Startall , not a persistent request.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       test.c



                                   1/9/2003                        MPI_Test(3)
```

### MPI_Testsome.md
```
MPI_Testsome(3)                       MPI                      MPI_Testsome(3)



NAME
       MPI_Testsome -  Tests for some given communications to complete

SYNOPSIS
       #include "mpi.h"
       int MPI_Testsome(
               int incount,
               MPI_Request array_of_requests[],
               int *outcount,
               int array_of_indices[],
               MPI_Status array_of_statuses[] )

INPUT PARAMETERS
       incount
              - length of array_of_requests (integer)
       array_of_requests
              - array of requests (array of handles)


OUTPUT PARAMETERS
       outcount
              - number of completed requests (integer)
       array_of_indices
              -  array of indices of operations that completed (array of inte-
              gers)
       array_of_statuses
              - array of status objects for operations that  completed  (array
              of Status).  May be MPI_STATUSES_IGNORE .



NOTE ON STATUS FOR SEND OPERATIONS
       For  send  operations, the only use of status is for MPI_Test_cancelled
       or in the case that there is an error,  in  which  case  the  MPI_ERROR
       field of status will be set.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_IN_STATUS
              -  The  actual  error value is in the MPI_Status argument.  This
              error  class  is  returned  only  from  the  multiple-completion
              routines  ( MPI_Testall , MPI_Testany , MPI_Testsome , MPI_Wait-
              all , MPI_Waitany , and MPI_Waitsome ).  The field MPI_ERROR  in
              the  status argument contains the error value or MPI_SUCCESS (no
              error and complete) or  MPI_ERR_PENDING  to  indicate  that  the
              request  has  not  completed.  The MPI Standard does not specify
              what the result of the multiple completion routines is  when  an
              error occurs.  For example, in an MPI_WAITALL , does the routine
              wait for all requests to either fail or  complete,  or  does  it
              return  immediately  (with  the  MPI  definition of immediately,
              which means independent of  actions  of  other  MPI  processes)?
              MPICH  has  chosen  to  make  the return immediate (alternately,
              local in MPI terms), and to use the error class  MPI_ERR_PENDING
              (introduced in MPI 1.1) to indicate which requests have not com-
              pleted.  In most cases, only one request with an error  will  be
              detected  in  each  call  to  an MPI routine that tests multiple
              requests.  The requests that have not been processed (because an
              error  occured in one of the requests) will have their MPI_ERROR
              field marked with MPI_ERR_PENDING .



LOCATION
       testsome.c



                                   1/9/2003                    MPI_Testsome(3)
```

### MPI_Topo_test.md
```
MPI_Topo_test(3)                      MPI                     MPI_Topo_test(3)



NAME
       MPI_Topo_test  -   Determines  the type of topology (if any) associated
       with a  communicator

SYNOPSIS
       #include "mpi.h"
       int MPI_Topo_test ( MPI_Comm comm, int *top_type )

INPUT PARAMETER
       comm   - communicator (handle)


OUTPUT PARAMETER
       top_type
              - topology type of communicator comm (choice).


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              - Invalid communicator.  A common error is to use a null  commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).


SEE ALSO
       MPI_Graph_create, MPI_Cart_create

LOCATION
       topo_test.c



                                  11/14/2001                  MPI_Topo_test(3)
```

### MPI_Type_commit.md
```
MPI_Type_commit(3)                    MPI                   MPI_Type_commit(3)



NAME
       MPI_Type_commit -  Commits the datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_commit ( MPI_Datatype *datatype )

INPUT PARAMETER
       datatype
              - datatype (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).

LOCATION
       type_commit.c



                                  11/14/2001                MPI_Type_commit(3)
```

### MPI_Type_contiguous.md
```
MPI_Type_contiguous(3)                MPI               MPI_Type_contiguous(3)



NAME
       MPI_Type_contiguous -  Creates a contiguous datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_contiguous(
               int count,
               MPI_Datatype old_type,
               MPI_Datatype *newtype)

INPUT PARAMETERS
       count  - replication count (nonnegative integer)
       oldtype
              - old datatype (handle)


OUTPUT PARAMETER
       newtype
              - new datatype (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.

LOCATION
       type_contig.c



                                  11/14/2001            MPI_Type_contiguous(3)
```

### MPI_Type_extent.md
```
MPI_Type_extent(3)                    MPI                   MPI_Type_extent(3)



NAME
       MPI_Type_extent -  Returns the extent of a datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_extent( MPI_Datatype datatype, MPI_Aint *extent )

INPUT PARAMETERS
       datatype
              - datatype (handle)


OUTPUT PARAMETER
       extent - datatype extent (integer)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).

LOCATION
       type_extent.c



                                  11/14/2001                MPI_Type_extent(3)
```

### MPI_Type_free.md
```
MPI_Type_free(3)                      MPI                     MPI_Type_free(3)



NAME
       MPI_Type_free -  Frees the datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_free ( MPI_Datatype *datatype )

INPUT PARAMETER
       datatype
              - datatype that is freed (handle)


PREDEFINED TYPES
       The MPI standard states that (in Opaque Objects)
       MPI provides certain predefined opaque objects and predefined, static handles
       to these objects. Such objects may not be destroyed.


       Thus,  it  is an error to free a predefined datatype.  The same section
       makes it clear that it is an error to free a null datatype.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       type_free.c



                                  11/14/2001                  MPI_Type_free(3)
```

### MPI_Type_hindexed.md
```
MPI_Type_hindexed(3)                  MPI                 MPI_Type_hindexed(3)



NAME
       MPI_Type_hindexed -  Creates an indexed datatype with offsets in bytes

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_hindexed(
               int count,
               int blocklens[],
               MPI_Aint indices[],
               MPI_Datatype old_type,
               MPI_Datatype *newtype )

INPUT PARAMETERS
       count  -  number  of  blocks  --  also number of entries in indices and
              blocklens
       blocklens
              - number of elements in each block (array of  nonnegative  inte-
              gers)
       indices
              - byte displacement of each block (array of MPI_Aint)
       old_type
              - old datatype (handle)


OUTPUT PARAMETER
       newtype
              - new datatype (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

       Also see the discussion for MPI_Type_indexed about the indices in  For-
       tran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       type_hind.c



                                   4/7/2003               MPI_Type_hindexed(3)
```

### MPI_Type_hvector.md
```
MPI_Type_hvector(3)                   MPI                  MPI_Type_hvector(3)



NAME
       MPI_Type_hvector  -  Creates a vector (strided) datatype with offset in
       bytes

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_hvector(
               int count,
               int blocklen,
               MPI_Aint stride,
               MPI_Datatype old_type,
               MPI_Datatype *newtype )

INPUT PARAMETERS
       count  - number of blocks (nonnegative integer)
       blocklength
              - number of elements in each block (nonnegative integer)
       stride - number of bytes between start of each block (integer)
       old_type
              - old datatype (handle)


OUTPUT PARAMETER
       newtype
              - new datatype (handle)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.

LOCATION
       type_hvec.c



                                  11/14/2001               MPI_Type_hvector(3)
```

### MPI_Type_indexed.md
```
MPI_Type_indexed(3)                   MPI                  MPI_Type_indexed(3)



NAME
       MPI_Type_indexed -  Creates an indexed datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_indexed(
               int count,
               int blocklens[],
               int indices[],
               MPI_Datatype old_type,
               MPI_Datatype *newtype )

INPUT PARAMETERS
       count  -  number  of  blocks  --  also number of entries in indices and
              blocklens
       blocklens
              - number of elements in each block (array of  nonnegative  inte-
              gers)
       indices
              -  displacement of each block in multiples of old_type (array of
              integers)
       old_type
              - old datatype (handle)


OUTPUT PARAMETER
       newtype
              - new datatype (handle)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

       The  indices are displacements, and are based on a zero origin.  A com-
       mon error is to do something like to following
       integer a(100)
       integer blens(10), indices(10)
       do i=1,10
       blens(i)   = 1
       10       indices(i) = 1 + (i-1)*10
       call MPI_TYPE_INDEXED(10,blens,indices,MPI_INTEGER,newtype,ierr)
       call MPI_TYPE_COMMIT(newtype,ierr)
       call MPI_SEND(a,1,newtype,...)

       expecting this to send a(1),a(11),...  because the indices have  values
       1,11,...   .  Because these are displacements from the beginning of a ,
       it actually sends a(1+1),a(1+11),...  .


       If you wish to consider the displacements as  indices  into  a  Fortran
       array, consider declaring the Fortran array with a zero origin
       integer a(0:99)



ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.

LOCATION
       type_ind.c



                                  11/14/2001               MPI_Type_indexed(3)
```

### MPI_Type_lb.md
```
MPI_Type_lb(3)                        MPI                       MPI_Type_lb(3)



NAME
       MPI_Type_lb -  Returns the lower-bound of a datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_lb ( MPI_Datatype datatype, MPI_Aint *displacement )

INPUT PARAMETERS
       datatype
              - datatype (handle)


OUTPUT PARAMETER
       displacement
              - displacement of lower bound from origin, in bytes (integer)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       type_lb.c



                                  11/14/2001                    MPI_Type_lb(3)
```

### MPI_Type_size.md
```
MPI_Type_size(3)                      MPI                     MPI_Type_size(3)



NAME
       MPI_Type_size  -  Return the number of bytes occupied by entries in the
       datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_size ( MPI_Datatype datatype, int *size )

INPUT PARAMETERS
       datatype
              - datatype (handle)


OUTPUT PARAMETER
       size   - datatype size (integer)


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       type_size.c



                                  11/14/2001                  MPI_Type_size(3)
```

### MPI_Type_struct.md
```
MPI_Type_struct(3)                    MPI                   MPI_Type_struct(3)



NAME
       MPI_Type_struct -  Creates a struct datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_struct(
               int count,
               int blocklens[],
               MPI_Aint indices[],
               MPI_Datatype old_types[],
               MPI_Datatype *newtype )

INPUT PARAMETERS
       count  - number of blocks (integer) -- also number of entries in arrays
              array_of_types  ,  array_of_displacements   and  array_of_block-
              lengths
       blocklens
              - number of elements in each block (array)
       indices
              - byte displacement of each block (array)
       old_types
              -  type  of elements in each block (array of handles to datatype
              objects)


OUTPUT PARAMETER
       newtype
              - new datatype (handle)


NOTES
       If an upperbound is set explicitly by using the MPI datatype  MPI_UB  ,
       the corresponding index must be positive.

       The  MPI  standard  originally  made vague statements about padding and
       alignment; this was intended to allow the simple definition  of  struc-
       tures that could be sent with a count greater than one.  For example,
       struct { int a; char b; } foo;

       may  have  sizeof(foo)  >  sizeof(int)  +  sizeof(char)  ; for example,
       sizeof(foo) == 2*sizeof(int) .  The initial version of the MPI standard
       defined  the  extent  of  a datatype as including an epsilon that would
       have allowed an implementation to make the extent an MPI  datatype  for
       this structure equal to 2*sizeof(int) .

       However, since different systems might define different paddings, there
       was much discussion by the MPI Forum about what was the  correct  value
       of  epsilon,  and  one  suggestion was to define epsilon as zero.  This
       would have been the best thing to do in MPI 1.0, particularly since the
       MPI_UB  type  allows  the  user to easily set the end of the structure.
       Unfortunately, this change did not make it  into  the  final  document.
       Currently,  this  routine does not add any padding, since the amount of
       padding needed is determined by the compiler that the user is using  to
       build  their  code, not the compiler used to construct the MPI library.
       A later version of MPICH  may  provide  for  some  natural  choices  of
       padding  (e.g.,  multiple of the size of the largest basic member), but
       users are advised to never depend on this, even with vendor MPI  imple-
       mentations.   Instead,  if  you define a structure datatype and wish to
       send or receive multiple items, you should explicitly include an MPI_UB
       entry  as the last member of the structure.  For example, the following
       code can be used for the structure foo
       blen[0] = 1; indices[0] = 0; oldtypes[0] = MPI_INT;
       blen[1] = 1; indices[1] = &foo.b - &foo; oldtypes[1] = MPI_CHAR;
       blen[2] = 1; indices[2] = sizeof(foo); oldtypes[2] = MPI_UB;
       MPI_Type_struct( 3, blen, indices, oldtypes, &newtype );



NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_INTERN
              - This error is returned when some part of the MPICH implementa-
              tion is unable to acquire memory.

LOCATION
       type_struct.c



                                   7/12/2002                MPI_Type_struct(3)
```

### MPI_Type_ub.md
```
MPI_Type_ub(3)                        MPI                       MPI_Type_ub(3)



NAME
       MPI_Type_ub -  Returns the upper bound of a datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_ub ( MPI_Datatype datatype, MPI_Aint *displacement )

INPUT PARAMETERS
       datatype
              - datatype (handle)


OUTPUT PARAMETER
       displacement
              - displacement of upper bound from origin, in bytes (integer)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       type_ub.c



                                  11/14/2001                    MPI_Type_ub(3)
```

### MPI_Type_vector.md
```
MPI_Type_vector(3)                    MPI                   MPI_Type_vector(3)



NAME
       MPI_Type_vector -  Creates a vector (strided) datatype

SYNOPSIS
       #include "mpi.h"
       int MPI_Type_vector(
               int count,
               int blocklen,
               int stride,
               MPI_Datatype old_type,
               MPI_Datatype *newtype )

INPUT PARAMETERS
       count  - number of blocks (nonnegative integer)
       blocklength
              - number of elements in each block (nonnegative integer)
       stride - number of elements between start of each block (integer)
       oldtype
              - old datatype (handle)


OUTPUT PARAMETER
       newtype
              - new datatype (handle)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.

LOCATION
       type_vec.c



                                  11/14/2001                MPI_Type_vector(3)
```

### MPI_Unpack.md
```
MPI_Unpack(3)                         MPI                        MPI_Unpack(3)



NAME
       MPI_Unpack -  Unpack a datatype into contiguous memory

SYNOPSIS
       #include "mpi.h"
       int MPI_Unpack ( void *inbuf, int insize, int *position,
                       void *outbuf, int outcount, MPI_Datatype datatype,
                       MPI_Comm comm )

INPUT PARAMETERS
       inbuf  - input buffer start (choice)
       insize - size of input buffer, in bytes (integer)
       position
              - current position in bytes (integer)
       outcount
              - number of items to be unpacked (integer)
       datatype
              - datatype of each output data item (handle)
       comm   - communicator for packed message (handle)


OUTPUT PARAMETER
       outbuf - output buffer start (choice)


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_COMM
              -  Invalid communicator.  A common error is to use a null commu-
              nicator in a call (not even allowed in MPI_Comm_rank ).
       MPI_ERR_COUNT
              - Invalid count argument.  Count arguments must be non-negative;
              a count of zero is often valid.
       MPI_ERR_TYPE
              - Invalid datatype argument.  May be an uncommitted MPI_Datatype
              (see MPI_Type_commit ).
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).


SEE ALSO
       MPI_Pack, MPI_Pack_size

LOCATION
       unpack.c



                                  11/14/2001                     MPI_Unpack(3)
```

### MPI_Waitall.md
```
MPI_Waitall(3)                        MPI                       MPI_Waitall(3)



NAME
       MPI_Waitall -  Waits for all given communications to complete

SYNOPSIS
       #include "mpi.h"
       int MPI_Waitall(
               int count,
               MPI_Request array_of_requests[],
               MPI_Status array_of_statuses[] )

INPUT PARAMETERS
       count  - lists length (integer)
       array_of_requests
              - array of requests (array of handles)


OUTPUT PARAMETER
       array_of_statuses
              -  array  of  status objects (array of Status).  May be MPI_STA-
              TUSES_IGNORE



NOTE ON STATUS FOR SEND OPERATIONS
       For send operations, the only use of status is  for  MPI_Test_cancelled
       or  in  the  case  that  there is an error, in which case the MPI_ERROR
       field of status will be set.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_REQUEST
              - Invalid MPI_Request .  Either  null  or,  in  the  case  of  a
              MPI_Start or MPI_Startall , not a persistent request.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_IN_STATUS
              - The actual error value is in the  MPI_Status  argument.   This
              error  class  is returned only from the multiple-completion rou-
              tines ( MPI_Testall , MPI_Testany , MPI_Testsome , MPI_Waitall ,
              MPI_Waitany  ,  and  MPI_Waitsome ).  The field MPI_ERROR in the
              status argument contains the  error  value  or  MPI_SUCCESS  (no
              error  and  complete)  or  MPI_ERR_PENDING  to indicate that the
              request has not completed.  The MPI Standard  does  not  specify
              what  the  result of the multiple completion routines is when an
              error occurs.  For example, in an MPI_WAITALL , does the routine
              wait  for  all  requests  to either fail or complete, or does it
              return immediately (with  the  MPI  definition  of  immediately,
              which  means  independent  of  actions  of other MPI processes)?
              MPICH has chosen to  make  the  return  immediate  (alternately,
              local  in MPI terms), and to use the error class MPI_ERR_PENDING
              (introduced in MPI 1.1) to indicate which requests have not com-
              pleted.   In  most cases, only one request with an error will be
              detected in each call to an  MPI  routine  that  tests  multiple
              requests.  The requests that have not been processed (because an
              error occured in one of the requests) will have their  MPI_ERROR
              field marked with MPI_ERR_PENDING .

       MPI_ERR_PENDING
              - Pending request (not an error).  See MPI_ERR_IN_STATUS .

              This  value indicates that the request is not complete nor has a
              encountered a detected error.

LOCATION
       waitall.c



                                   2/24/2004                    MPI_Waitall(3)
```

### MPI_Waitany.md
```
MPI_Waitany(3)                        MPI                       MPI_Waitany(3)



NAME
       MPI_Waitany -  Waits for any specified send or receive to complete

SYNOPSIS
       #include "mpi.h"
       int MPI_Waitany(
               int count,
               MPI_Request array_of_requests[],
               int *index,
               MPI_Status *status )

INPUT PARAMETERS
       count  - list length (integer)
       array_of_requests
              - array of requests (array of handles)


OUTPUT PARAMETERS
       index  -  index  of  handle for operation that completed (integer).  In
              the range 0 to count-1 .  In Fortran, the range is 1 to count  .

       status - status object (Status).  May be MPI_STATUS_IGNORE .



NOTES
       If all of the requests are MPI_REQUEST_NULL , then index is returned as
       MPI_UNDEFINED , and status is returned as an empty status.


NOTE ON STATUS FOR SEND OPERATIONS
       For send operations, the only use of status is  for  MPI_Test_cancelled
       or  in  the  case  that  there is an error, in which case the MPI_ERROR
       field of status will be set.


NOTES FOR FORTRAN
       All MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK )  have
       an  additional  argument ierr at the end of the argument list.  ierr is
       an integer and has the same meaning as the return value of the  routine
       in  C.   In Fortran, MPI routines are subroutines, and are invoked with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All  MPI  routines  (except  MPI_Wtime  and MPI_Wtick ) return an error
       value; C routines as the value of the function and Fortran routines  in
       the last argument.  Before the value is returned, the current MPI error
       handler is called.  By default, this error handler aborts the MPI  job.
       The  error  handler may be changed with MPI_Errhandler_set ; the prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to  be  returned.  Note that MPI does not guarentee that an MPI program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_REQUEST
              - Invalid MPI_Request .  Either  null  or,  in  the  case  of  a
              MPI_Start or MPI_Startall , not a persistent request.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       waitany.c



                                   1/9/2003                     MPI_Waitany(3)
```

### MPI_Wait.md
```
MPI_Wait(3)                           MPI                          MPI_Wait(3)



NAME
       MPI_Wait -  Waits for an MPI send or receive to complete

SYNOPSIS
       #include "mpi.h"
       int MPI_Wait (
               MPI_Request  *request,
               MPI_Status   *status)

INPUT PARAMETER
       request
              - request (handle)


OUTPUT PARAMETER
       status - status object (Status) .  May be MPI_STATUS_IGNORE .



NOTE ON STATUS FOR SEND OPERATIONS
       For  send  operations, the only use of status is for MPI_Test_cancelled
       or in the case that there is an error,  in  which  case  the  MPI_ERROR
       field of status will be set.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_REQUEST
              -  Invalid  MPI_Request  .   Either  null  or,  in the case of a
              MPI_Start or MPI_Startall , not a persistent request.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).

LOCATION
       wait.c



                                   1/9/2003                        MPI_Wait(3)
```

### MPI_Waitsome.md
```
MPI_Waitsome(3)                       MPI                      MPI_Waitsome(3)



NAME
       MPI_Waitsome -  Waits for some given communications to complete

SYNOPSIS
       #include "mpi.h"
       int MPI_Waitsome(
               int incount,
               MPI_Request array_of_requests[],
               int *outcount,
               int array_of_indices[],
               MPI_Status array_of_statuses[] )

INPUT PARAMETERS
       incount
              - length of array_of_requests (integer)
       array_of_requests
              - array of requests (array of handles)


OUTPUT PARAMETERS
       outcount
              - number of completed requests (integer)
       array_of_indices
              -  array of indices of operations that completed (array of inte-
              gers)
       array_of_statuses
              - array of status objects for operations that  completed  (array
              of Status).  May be MPI_STATUSES_IGNORE .



NOTES
       The  array  of  indicies are in the range 0 to incount - 1 for C and in
       the range 1 to incount for Fortran.

       Null requests are ignored; if all requests are null, then  the  routine
       returns with outcount set to MPI_UNDEFINED .



NOTE ON STATUS FOR SEND OPERATIONS
       For  send  operations, the only use of status is for MPI_Test_cancelled
       or in the case that there is an error,  in  which  case  the  MPI_ERROR
       field of status will be set.


NOTES FOR FORTRAN
       All  MPI routines in Fortran (except for MPI_WTIME and MPI_WTICK ) have
       an additional argument ierr at the end of the argument list.   ierr  is
       an  integer and has the same meaning as the return value of the routine
       in C.  In Fortran, MPI routines are subroutines, and are  invoked  with
       the call statement.

       All MPI objects (e.g., MPI_Datatype , MPI_Comm ) are of type INTEGER in
       Fortran.


ERRORS
       All MPI routines (except MPI_Wtime and  MPI_Wtick  )  return  an  error
       value;  C routines as the value of the function and Fortran routines in
       the last argument.  Before the value is returned, the current MPI error
       handler  is called.  By default, this error handler aborts the MPI job.
       The error handler may be changed with MPI_Errhandler_set ;  the  prede-
       fined error handler MPI_ERRORS_RETURN may be used to cause error values
       to be returned.  Note that MPI does not guarentee that an  MPI  program
       can continue past an error.

       MPI_SUCCESS
              - No error; MPI routine completed successfully.
       MPI_ERR_REQUEST
              -  Invalid  MPI_Request  .   Either  null  or,  in the case of a
              MPI_Start or MPI_Startall , not a persistent request.
       MPI_ERR_ARG
              - Invalid argument.  Some argument is invalid and is not identi-
              fied by a specific error class (e.g., MPI_ERR_RANK ).
       MPI_ERR_IN_STATUS
              -  The  actual  error value is in the MPI_Status argument.  This
              error class is returned only from the  multiple-completion  rou-
              tines ( MPI_Testall , MPI_Testany , MPI_Testsome , MPI_Waitall ,
              MPI_Waitany , and MPI_Waitsome ).  The field  MPI_ERROR  in  the
              status  argument  contains  the  error  value or MPI_SUCCESS (no
              error and complete) or  MPI_ERR_PENDING  to  indicate  that  the
              request  has  not  completed.  The MPI Standard does not specify
              what the result of the multiple completion routines is  when  an
              error occurs.  For example, in an MPI_WAITALL , does the routine
              wait for all requests to either fail or  complete,  or  does  it
              return  immediately  (with  the  MPI  definition of immediately,
              which means independent of  actions  of  other  MPI  processes)?
              MPICH  has  chosen  to  make  the return immediate (alternately,
              local in MPI terms), and to use the error class  MPI_ERR_PENDING
              (introduced in MPI 1.1) to indicate which requests have not com-
              pleted.  In most cases, only one request with an error  will  be
              detected  in  each  call  to  an MPI routine that tests multiple
              requests.  The requests that have not been processed (because an
              error  occured in one of the requests) will have their MPI_ERROR
              field marked with MPI_ERR_PENDING .


LOCATION
       waitsome.c



                                   1/9/2003                    MPI_Waitsome(3)
```

### MPI_Wtick.md
```
MPI_Wtick(3)                          MPI                         MPI_Wtick(3)



NAME
       MPI_Wtick -  Returns the resolution of MPI_Wtime

SYNOPSIS
       #include "mpi.h"
       double MPI_Wtick()

RETURN VALUE
       Time in seconds of the resolution of MPI_Wtime .


NOTES FOR FORTRAN
       This  is  a  function, declared as DOUBLE PRECISION MPI_WTICK() in For-
       tran.


LOCATION
       wtick.c



                                   8/20/2004                      MPI_Wtick(3)
```

### MPI_Wtime.md
```
MPI_Wtime(3)                          MPI                         MPI_Wtime(3)



NAME
       MPI_Wtime -  Returns an elapsed time on the calling processor

SYNOPSIS
       #include "mpi.h"
       double MPI_Wtime()

RETURN VALUE
       Time in seconds since an arbitrary time in the past.


NOTES
       This is intended to be a high-resolution, elapsed (or wall) clock.  See
       MPI_WTICK to determine the resolution of MPI_WTIME .

       If the attribute MPI_WTIME_IS_GLOBAL is  defined  and  true,  then  the
       value is synchronized across all processes in MPI_COMM_WORLD .



NOTES FOR FORTRAN
       This  is  a  function, declared as DOUBLE PRECISION MPI_WTIME() in For-
       tran.


SEE ALSO
       also: MPI_Wtick, MPI_Attr_get

LOCATION
       wtime.c



                                  11/14/2001                      MPI_Wtime(3)
```
