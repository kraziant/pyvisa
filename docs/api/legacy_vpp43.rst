.. _legacy_vpp43:


:mod:`legacy.vpp43` functions
-----------------------------

Please note that all descriptions given in this reference serve mostly as
reminders.  For real descriptions consult a `VISA specification`_ or `NI-VISA
Programmer Reference Manual`_.  However, whenever there are PyVISA-specific
semantics, they are listed here, too.

.. _`VISA specification`:
       http://www.ivifoundation.org/Downloads/Class%20Specifications/vpp43.doc
.. _`NI-VISA Programmer Reference Manual`:
       http://digital.ni.com/manuals.nsf/websearch/87E52268CF9ACCEE86256D0F006E860D

assert_interrupt_signal
.......................

Asserts the specified device interrupt or signal.

:Call: assert_interrupt_signal(vi, mode, status_id)
:VISA name: viAssertIntrSignal
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `mode` : integer
        This specifies how to assert the interrupt.
    `status_id` : integer
        This is the status value to be presented during an interrupt
        acknowledge cycle.
:Return values:
    None.


assert_trigger
..............

Assert software or hardware trigger.

:Call: assert_trigger(vi, protocol)
:VISA name: viAssertTrigger
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `protocol` : integer
        Trigger protocol to use during assertion.  Valid values are:
        ``VI_TRIG_PROT_DEFAULT``, ``VI_TRIG_PROT_ON``, ``VI_TRIG_PROT_OFF``,
        and ``VI_TRIG_PROT_SYNC``.
:Return values:
    None.


assert_utility_signal
.....................

Asserts the specified utility bus signal.

:Call: assert_utility_signal(vi, line)
:VISA name: viAssertUtilSignal
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `line` : integer
        Specifies the utility bus signal to assert.
:Return values:
    None.


buffer_read
...........

Similar to `read`_, except that the operation uses the formatted I/O read
buffer for holding data read from the device.

:Call: buffer = buffer_read(vi, count)
:VISA name: viBufRead
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `count` : integer
        Maximal number of bytes to be read.
:Return values:
    `buffer` : string
        The buffer with the received data from device.


buffer_write
............

Similar to `write`_, except the data is written to the formatted I/O write
buffer rather than directly to the device.

:Call: return_count = buffer_write(vi, buffer)
:VISA name: viBufWrite
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `buffer` : string
        The data block to be sent to device.
:Return values:
    `return_count` : integer
        The number of bytes actually transferred.


clear
.....

Clear a device.

:Call: clear(vi)
:VISA name: viClear
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
:Return values:
    None.


close
.....

Close the specified session, event, or find list.

:Call: close(vi)
:VISA name: viClose
:Parameters:
    `vi` : integer, ViEvent, or ViFindList
        Unique logical identifier to a session, event, or find list.
:Return values:
    None.


disable_event
.............

Disable notification of an event type by the specified mechanisms.

:Call: disable_event(vi, event_type, mechanism)
:VISA name: viDisableEvent
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `event_type` : integer
        Logical event identifier.
    `mechanism` : integer
        Specifies event handling mechanisms to be disabled. The queuing
        mechanism is disabled by specifying ``VI_QUEUE``, and the callback
        mechanism is disabled by specifying ``VI_HNDLR`` or
        ``VI_SUSPEND_HNDLR``. It is possible to disable both mechanisms
        simultaneously by specifying ``VI_ALL_MECH``.
:Return values:
    None.


discard_events
..............

Discard event occurrences for specified event types and mechanisms in a
session.

:Call: discard_events(vi, event_type, mechanism)
:VISA name: viDiscardEvents
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `event_type` : integer
        Logical event identifier.
    `mechanism` : integer
        Specifies the mechanisms for which the events are to be discarded.  The
        ``VI_QUEUE`` value is specified for the queuing mechanism and the
        ``VI_SUSPEND_HNDLR`` value is specified for the pending events in the
        callback mechanism.  It is possible to specify both mechanisms
        simultaneously by specifying ``VI_ALL_MECH``.
:Return values:
    None.


enable_event
............

Enable notification of a specified event.

:Call: enable_event(vi, event_type, mechanism, context)
:VISA name: viEnableEvent
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `event_type` : integer
        Logical event identifier.
    `mechanism` : integer
        Specifies event handling mechanisms to be enabled.  The queuing
        mechanism is enabled by specifying ``VI_QUEUE``, and the callback
        mechanism is enabled by specifying ``VI_HNDLR`` or
        ``VI_SUSPEND_HNDLR``.  It is possible to enable both mechanisms
        simultaneously by specifying bit-wise "or" of ``VI_QUEUE`` and one of
        the two mode values for the callback mechanism.
    `context` : integer : optional
        According to the VISA specification, this must be ``Vi_NULL`` always.
        (This is also the default value, of course.)
:Return values:
    None.


find_next
.........

:Call: instrument_description = find_next(find_list)
:VISA name: viFindNext
:Parameters:
    `find_list` : ViFindList
        Describes a find list.  This parameter must be created by
        `find_resources`_.
:Return values:
    `instrument_description` : string
        Returns a string identifying the location of a device. Strings can then
        be passed to `open`_ to establish a session to the given device.


find_resources
..............

:Call: find_list, return_counter, instrument_description =
       find_resources(session, regular_expression)
:VISA name: viFindRsrc
:Parameters:
    `session` : integer
        Resource Manager session (should always be the Default Resource Manager
        for VISA returned from `open_default_resource_manager`_).
    `regular_expression` : integer
        This is a regular expression followed by an optional logical
        expression.
:Return values:
    `find_list` : ViFindList
        Returns a handle identifying this search session. This handle will be
        used as an input in `find_next`_.
    `return_counter` : integer
        Number of matches.
    `instrument_description` : string
        Returns a string identifying the location of a device. Strings can then
        be passed to `open`_ to establish a session to the given device.


flush
.....

Manually flush the specified buffers associated with formatted I/O operations
and/or serial communication.

:Call: flush(vi, mask)
:VISA name: viFlush
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `mask` : integer
        Specifies the action to be taken with flushing the buffer.
:Return values:
    None.


get_attribute
.............

Retrieve the state of an attribute.

:Call: attribute_state = get_attribute(vi, attribute)
:VISA name: viGetAttribute
:Parameters:
    `vi` : integer, ViEvent, or ViFindList
        Unique logical identifier to a session.
    `attribute` : integer
        Session, event, or find list attribute for which the state query is
        made.
:Return values:
    `attribute_state` : integer, string, or list of integers
        The state of the queried attribute for a specified resource.


gpib_command
............

Write GPIB command bytes on the bus.

:Call: return_count = gpib_command(vi, buffer)
:VISA name: viGpibCommand
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `buffer` : string
        Buffer containing valid GPIB commands.
:Return values:
    `return_count` : integer
        Number of bytes actually transferred.


gpib_control_atn
................

Controls the state of the GPIB ATN interface line, and optionally the active
controller state of the local interface board.

:Call: gpib_control_atn(vi, mode)
:VISA name: viGpibControlATN
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `mode` : integer
        Specifies the state of the ATN line and optionally the local active
        controller state. See the Description section for actual values.

:Return values:
    None.


gpib_control_ren
................

Controls the state of the GPIB REN interface line, and optionally the
remote/local state of the device.

:Call: gpib_control_ren(vi, mode)
:VISA name: viGpibControlREN
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `mode` : integer
        Specifies the state of the REN line and optionally the device
        remote/local state. See the Description section for actual values.

:Return values:
    None.


gpib_pass_control
.................

Tell the GPIB device at the specified address to become controller in charge
(CIC).

:Call: gpib_pass_control(vi, primary_address, secondary_address)
:VISA name: viGpibPassControl
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `primary_address` : integer
        Primary address of the GPIB device to which you want to pass control.
    `secondary_address` : integer
        Secondary address of the targeted GPIB device. If the targeted device
        does not have a secondary address, this parameter should contain the
        value ``VI_NO_SEC_ADDR``.

:Return values:
    None.


gpib_send_ifc
.............

Pulse the interface clear line (IFC) for at least 100 microseconds.

:Call: gpib_send_ifc(vi)
:VISA name: viGpibSendIFC
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.

:Return values:
    None.


in_8, in_16, in_32
..................

Read in an 8-bit, 16-bit, or 32-bit value from the specified memory space and
offset.

:Call: | value_8 = in_8(vi, space, offset)
       | value_16 = in_16(vi, space, offset)
       | value_32 = in_32(vi, space, offset)
:VISA name: viIn8, viIn16, viIn32
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `space` : integer
        Specifies the address space.
    `offset` : integer
        Offset in bytes of the address or register from which to read.
:Return values:
    `value_8`, `value_16`, `value_32` : integer
        Data read from bus (8 bits for `in_8`, 16 bits for `in_16`, and 32
        bits for `in_32`).


install_handler
...............

Install handlers for event callbacks.  A handler must have the following
signature::

    def event_handler(vi, event_type, context, user_handle):
        ...

Its parameters mean the following:

`vi` : integer
    Unique logical identifier to a session.
`event_type` : ViEvent
    Logical event identifier.  With ``event_type.value`` you get its value as
    an integer.
`context` : ViEvent
    A handle specifying the unique occurrence of an event.
`user_handle` : ctypes pointer type
    A *pointer* to the user handle in ctypes form.  See below at "Return
    values" for how to use it, however, you have to substitute
    ``user_handle.contents`` for ``converted_user_handle`` in the explanation.

:Call: converted_user_handle = install_handler(vi, event_type, handler,
       user_handle)
:VISA name: viInstallHandler
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `event_type` : integer
        Logical event identifier.
    `handler` : callable
        Interpreted as a valid reference to a handler to be installed by a
        client application.
    `user_handle` : ``None``, float, integer, string, or list of floats or integers : optional
        A value specified by an application that can be used for identifying
        handlers uniquely for an event type.  It defaults to ``None``.
:Return values:
    `converted_user_handle` : ctypes type
        An object representing the user_handle.  Use it to communicate with
        your handler.  If your user_handle was a list, you get its elements as
        usual with ``converted_user_handle[index]``.  You can even convert it
        to a list with ``list(converted_user_handle)`` (however, this yields a
        copy).

        For strings, use ``converted_user_handle.value`` if it's supposed to be
        interpreted as a null-terminated string, or
        ``converted_user_handle.raw`` if you want to see *all* bytes.  You can
        also write to both expressions, however, slicing is only possible for
        reading.

        For simple types, you can say ``converted_user_handle.value`` (read and
        write).

        **Attention:** You must assure that you never write values to
        converted_user_data which are longer (in bytes) than the initial
        values.  So be careful not to write a string longer than the original
        one, nor a longer list.  You'd be alerted by exceptions, though.


lock
....

Establish an access mode to the specified resource.

:Call: access_key = lock(vi, lock_type, timeout, requested_key)
:VISA name: viLock
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `lock_type` : integer
        Specifies the type of lock requested, which can be either
        ``VI_EXCLUSIVE_LOCK`` or ``VI_SHARED_LOCK``.
    `timeout` : integer
        Absolute time period in milliseconds that a resource waits to get
        unlocked by the locking session before returning this operation with an
        error.
    `requested_key` : ctypes string : optional
        This parameter is not used if `lock_type` is ``VI_EXCLUSIVE_LOCK``
        (exclusive locks).  When trying to lock the resource as
        ``VI_SHARED_LOCK`` (shared), you can either omit it so that VISA
        generates an `access_key` for the session, or you can suggest an
        `access_key` to use for the shared lock.
:Return values:
    `access_key` : ctypes string : optional
        This value is ``None`` if `lock_type` is ``VI_EXCLUSIVE_LOCK``
        (exclusive locks).  When trying to lock the resource as
        ``VI_SHARED_LOCK`` (shared), the function returns a unique access key
        for the lock if the operation succeeds.  This `access_key` can then be
        passed to other sessions to share the lock.


map_address
...........

Map the specified memory space into the process's address space.

:Call: address = map_address(vi, map_space, map_base, map_size, access,
       suggested)
:VISA name: viMapAddress
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `map_space` : integer
        Specifies the address space to map.
    `map_base` : ViBusAddress
        Offset in bytes of the memory to be mapped.
    `map_size` : integer
        Amount of memory to map in bytes.
    `access` : integer : optional
        Must be ``VI_FALSE``.
    `suggested` : integer : optional
        If not ``VI_NULL`` (the default), the operating system attempts to map
        the memory to the address specified in suggested. There is no
        guarantee, however, that the memory will be mapped to that
        address. This operation may map the memory into an address region
        different from suggested.
:Return values:
    `address` : ViAddr
        Address in your process space where the memory was mapped.


map_trigger
...........

Map the specified trigger source line to the specified destination line.

:Call: map_trigger(vi, trigger_source, trigger_destination, mode)
:VISA name: viMapTrigger
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `trigger_source` : integer
        Source line from which to map.
    `trigger_destination` : integer
        Destination line to which to map.
    `mode` : integer
        Specifies the trigger mapping mode. This should always be VI_NULL.
:Return values:
    None.


memory_allocation
.................

Allocate memory from a device's memory region.

:Call: memory_allocation(vi, size)
:VISA name: viMemAlloc
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `size` : integer
        Specifies the size of the allocation.
:Return values:
    offset : ViBusAddress
        Returns the offset of the allocated device memory.


memory_free
...........

Free memory previously allocated using `memory_allocation`_.

:Call: memory_free(vi, offset)
:VISA name: viMemFree
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `offset` : ViBusAddress
        Specifies the memory previously allocated with `memory_allocation`_.
:Return values:
    None.


move
....

Move a block of data.

:Call: move(vi, source_space, source_offset, source_width, destination_space,
         destination_offset, destination_width, length)
:VISA name: viMove
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `source_space` : integer
        Specifies the address space of the source.
    `source_offset` : integer
        Offset in bytes of the starting address or register from which to
        read.
    `source_width` : integer
        Specifies the data width of the source.
    `destination_space` : integer
        Specifies the address space of the destination.
    `destination_offset` : integer
        Offset in bytes of the starting address or register to which to write.
    `destination_width` : integer
        Specifies the data width of the destination.
    `length` : integer
        Number of elements to transfer, where the data width of the elements to
        transfer is identical to source data width.
:Return values:
    None.


move_asynchronously
...................

Move a block of data asynchronously.

:Call: job_id = move_asynchronously(vi, source_space, source_offset,
       source_width, destination_space, destination_offset, destination_width,
       length)
:VISA name: viMoveAsync
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `source_space` : integer
        Specifies the address space of the source.
    `source_offset` : integer
        Offset in bytes of the starting address or register from which to
        read.
    `source_width` : integer
        Specifies the data width of the source.
    `destination_space` : integer
        Specifies the address space of the destination.
    `destination_offset` : integer
        Offset in bytes of the starting address or register to which to write.
    `destination_width` : integer
        Specifies the data width of the destination.
    `length` : integer
        Number of elements to transfer, where the data width of the elements to
        transfer is identical to source data width.
:Return values:
    `job_id` : ViJobId
        The job identifier of this asynchronous move operation. Each time an
        asynchronous move operation is called, it is assigned a unique job
        identifier.


move_in_8, move_in_16, move_in_32
.................................

Move a block of data from the specified address space and offset to local
memory in increments of 8, 16, or 32 bits.

:Call: | buffer_8 = move_in_8(vi, space, offset, length)
       | buffer_16 = move_in_16(vi, space, offset, length)
       | buffer_32 = move_in_32(vi, space, offset, length)
:VISA name: viMoveIn8, viMoveIn16, viMoveIn32
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `space` : integer
        Specifies the address space.
    `offset` : ViBusAddress
        Offset in bytes of the starting address or register from which to
        read.
    `length` : integer
        Number of elements to transfer, where the data width of the elements to
        transfer is identical to data width (8, 16, or 32 bits).
:Return values:
    `buffer_8`, `buffer_16`, `buffer_32` : list of integers
        Data read from bus as a Python list of values.


move_out_8, move_out_16, move_out_32
....................................

Move a block of data from local memory to the specified address space and
offset in increments of 8, 16, or 32 bits.

:Call: | move_out_8(vi, space, offset, length, buffer_8)
       | move_out_16(vi, space, offset, length, buffer_16)
       | move_out_32(vi, space, offset, length, buffer_32)
:VISA name: viMoveOut8, viMoveOut16, viMoveOut32
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `space` : integer
        Specifies the address space.
    `offset` : ViBusAddress
        Offset in bytes of the starting address or register from which to
        write.
    `length` : integer
        Number of elements to transfer, where the data width of the elements to
        transfer is identical to data width (8, 16, or 32 bits).
    `buffer_8`, `buffer_16`, `buffer_32` : sequence of integers
        Data to write to bus.  This may be a list or a tuple, however in any
        case in must contain integers.
:Return values:
    None.


open
....

Open a session to the specified device.

:Call: vi = open(session, resource_name, access_mode, open_timeout)
:VISA name: viOpen
:Parameters:
    `session` : integer
        Resource Manager session (should always be the Default Resource Manager
        for VISA returned from `open_default_resource_manager`_).
    `resource_name` : string
        Unique symbolic name of a resource.
    `access_mode` : integer : optional
        Defaults to ``VI_NO_LOCK``.  Specifies the modes by which the resource
        is to be accessed.  The value ``VI_EXCLUSIVE_LOCK`` is used to acquire
        an exclusive lock immediately upon opening a session; if a lock cannot
        be acquired, the session is closed and an error is returned.  The value
        ``VI_LOAD_CONFIG`` is used to configure attributes to values specified
        by some external configuration utility; if this value is not used, the
        session uses the default values provided by this
        specification.  Multiple access modes can be used simultaneously by
        specifying a "bitwise OR" of the above values.
    `open_timeout` : integer : optional
        If the `access_mode` parameter requests a lock, then this parameter
        specifies the absolute time period in milliseconds that the resource
        waits to get unlocked before this operation returns an error;
        otherwise, this parameter is ignored.  Defaults to
        ``VI_TMO_IMMEDIATE``.
:Return values:
    `vi` : integer
        Unique logical identifier reference to a session.


open_default_resource_manager
.............................

Return a session to the Default Resource Manager resource.

:Call: session = open_default_resource_manager()
:VISA name: viOpenDefaultRM
:Parameters:
    None.
:Return values:
    `session` : integer
        Unique logical identifier to a Default Resource Manager session.


get_default_resource_manager
............................

This is a deprecated alias for `open_default_resource_manager`_.


out_8, out_16, out_32
.....................

:Call: | out_8(vi, space, offset, value_8)
       | out_16(vi, space, offset, value_16)
       | out_32(vi, space, offset, value_32)
:VISA name: viOut8, viOut16, viOut32
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `space` : integer
        Specifies the address space.
    `offset` : integer
        Offset in bytes of the address or register to which to write.
    `value_8`, `value_16`, `value_32`: integer
        Data to write to bus (8 bits for out_8, 16 bits for out_16, and 32 bits
        for out_32).
:Return values:
    None.


parse_resource
..............

Parse a resource string to get the interface information.

:Call: interface_type, interface_board_number = parse_resource(session,
       resource_name)
:VISA name: viParseRsrc
:Parameters:
    `session` : integer
        Resource Manager session (should always be the Default Resource Manager
        for VISA returned from `open_default_resource_manager`_).
    `resource_name` : string
        Unique symbolic name of a resource.
:Return values:
    `interface_type` : integer
        Interface type of the given resource string.
    `interface_board_number` : integer
        Board number of the interface of the given resource string.


parse_resource_extended
.......................

Parse a resource string to get extended interface information.

**Attention:** Calling this function may raise an ``AttributeError`` because
some older VISA implementation don't have the function ``viParseRsrcEx``.

:Call: interface_type, interface_board_number, resource_class,
       unaliased_expanded_resource_name, alias_if_exists =
       parse_resource_extended(session, resource_name)
:VISA name: viParseRsrcEx
:Parameters:
    `session` : integer
        Resource Manager session (should always be the Default Resource Manager
        for VISA returned from `open_default_resource_manager`_).
    `resource_name` : string
        Unique symbolic name of a resource.
:Return values:
    `interface_type` : integer
        Interface type of the given resource string.
    `interface_board_number` : integer
        Board number of the interface of the given resource string.
    `resource_class` : string
        Specifies the resource class (for example "INSTR") of the given
        resource string.
    `unaliased_expanded_resource_name` : string
        This is the expanded version of the given resource string. The format
        should be similar to the VISA-defined canonical resource name.
    `alias_if_exists` : string
        Specifies the user-defined alias for the given resource string, if a
        VISA implementation allows aliases and an alias exists for the given
        resource string.  If not, this is ``None``.


peek_8, peek_16, peek_32
........................

Read an 8-bit, 16-bit, or 32-bit value from the specified address.

:Call: | value_8 = peek_8(vi, address)
       | value_16 = peek_16(vi, address)
       | value_32 = peek_32(vi, address)
:VISA name: viPeek8, viPeek16, viPeek32
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `address` : ViAddr
        Specifies the source address to read the value.
:Return values:
    `value_8`, `value_16`, `value_32` : integer
        Data read from bus (8 bits for peek_8, 16 bits for peek_16, and 32 bits
        for peek_32).


poke_8, poke_16, poke_32
........................

Write an 8-bit, 16-bit, or 32-bit value to the specified address.

:Call: | poke_8(vi, address, value_8)
       | poke_16(vi, address, value_16)
       | poke_32(vi, address, value_32)
:VISA name: vipoke_8
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `address` : integer
        Specifies the destination address to store the value.
    `value_8`, `value_16`, `value_32` : integer
        Data to write to bus (8 bits for poke_8, 16 bits for poke_16, and 32
        bits for poke_32).
:Return values:
    None.


printf
......

Convert, format, and send the parameters ``...`` to the device as specified by
the format string.

.. Warning::
    The current implementation only supports the following C data types:
    ``long``, ``double`` and ``char*`` (strings).  Thus, you can only use these
    three data types in format strings for printf, scanf and the like.

:Call: printf(vi, write_format, ...)
:VISA name: viPrintf
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `write_format` : string
        String describing the format for arguments.
    `...` : integers, floats, or strings
        Arguments sent to the device according to `write_format`.
:Return values:
    None.


queryf
......

Perform a formatted write and read through a single operation invocation.

.. Warning::
    The current implementation only supports the following C data types:
    ``long``, ``double`` and ``char*`` (strings).  Thus, you can only use these
    three data types in format strings for printf, scanf and the like.

:Call: value1, value2, ... = queryf(vi, write_format, read_format, (...), ...,
       maximal_string_length = 1024)
:VISA name: viQueryf
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `write_format` : string
        String describing the format for arguments.
    `read_format` : string
        String describing the format for arguments.
    `(...)` : tuple of integers, floats, or strings
        Arguments sent to the device according to `write_format`.  May be
        ``None``.
    `...` : integers, floats, or strings
        Arguments to be read from the device according to `read_format`.  It's
        totally insignificant which values they have, they serve just as a
        cheap way to determine what types are to be expected.  So actually this
        argument list shouldn't be necessary, but with the current
        implementation, it is, sorry.

        These arguments may be (however needn't be) the same names used for
        storing the result values.  Alternatively, you can give literals.
    `maximal_string_length` : integer : keyword argument
        The maximal length assumed for string result arguments.  Note that
        string results must *never* exceed this length.  It defaults to 1024.
:Return values:
    `value1`, `value2`, ... : integers, floats, or strings
        Arguments read from the device according to `read_format`.  Of course,
        this must be the same sequence (as far as data types are concerned) as
        the given argument list `...` above.


read
....

Read data from device synchronously.

:Call: buffer = read(vi, count)
:VISA name: viRead
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `count` : integer
        Maximal number of bytes to be read.
:Return values:
    `buffer` : string
        Represents the buffer with the received data from device.


read_asynchronously
...................

Read data from device asynchronously.

:Call: buffer, job_id = read_asynchronously(vi, count)
:VISA name: viReadAsync
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `count` : integer
        Maximal number of bytes to be read.
:Return values:
    `buffer` : ctypes string buffer
        Represents the buffer with the data received from device.  It's not a
        native Python data type because it's filled in the background
        (i.e. asynchronously).  After you assured that the reading is finished,
        you get its value with::

            buffer.raw[:return_count]

        You get ``return_count`` via the attribute ``VI_ATTR_RET_COUNT``.  See
        the `VISA reference`_ for further information.
    `job_id` : ViJobId
        Represents the location of a variable that will be set to the job
        identifier of this asynchronous read operation.

.. _`VISA reference`:
       http://digital.ni.com/manuals.nsf/websearch/87E52268CF9ACCEE86256D0F006E860D


read_stb
........

Read a status byte of the service request.

:Call: status = read_stb(vi)
:VISA name: viReadSTB
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
:Return values:
    `status` : integer
        Service request status byte.


read_to_file
............

Read data synchronously, and store the transferred data in a file.

:Call: return_count = read_to_file(vi, filename, count)
:VISA name: viReadToFile
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `file_name` : string
        Name of file to which data will be written.
    `count` : integer
        Maximal number of bytes to be read.
:Return values:
    `return_count` : integer
        Number of bytes actually transferred.


scanf
.....

Read, convert, and format data using the format specifier.  Store the formatted
data in the given optional parameters.

.. Warning::
    The current implementation only supports the following C data types:
    ``long``, ``double`` and ``char*`` (strings).  Thus, you can only use these
    three data types in format strings for printf, scanf and the like.

:Call: value1, value2, ... = scanf(vi, read_format, ..., maximal_string_length
       = 1024)
:VISA name: viScanf
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `read_format` : string
        String describing the format for arguments.
    `...` : integers, floats, or strings
        Arguments to be read from the device according to `read_format`.  It's
        totally insignificant which values they have, they serve just as a
        cheap way to determine what types are to be expected.  So actually this
        argument list shouldn't be necessary, but with the current
        implementation, it is, sorry.

        These arguments may be (however needn't be) the same names used for
        storing the result values.  Alternatively, you can give literals.
    `maximal_string_length` : integer : keyword argument
        The maximal length assumed for string result arguments.  Note that
        string results must *never* exceed this length.  It defaults to 1024.
:Return values:
    `value1`, `value2`, ... : integers, floats, or strings
        Arguments read from the device according to `read_format`.  Of course,
        this must be the same sequence (as far as data types are concerned) as
        the given argument list `...` above.


set_attribute
.............

Set the state of an attribute.

:Call: set_attribute(vi, attribute, attribute_state)
:VISA name: viSetAttribute
:Parameters:
    `vi` : integer, ViEvent, or ViFindList
        Unique logical identifier to a session.
    `attribute` : integer
        Session, event, or find list attribute for which the state is
        modified.
    `attribute_state` : integer
        The state of the attribute to be set for the specified resource.  The
        interpretation of the individual attribute value is defined by the
        resource.
:Return values:
    None.


set_buffer
..........

Set the size for the formatted I/O and/or serial communication buffer(s).

:Call: set_buffer(vi, mask, size)
:VISA name: viSetBuf
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `mask` : integer
        Specifies the type of buffer.
    `size` : integer
        The size to be set for the specified buffer(s).
:Return values:
    None.


sprintf
.......

Same as `printf`_, except the data is written to a user-specified buffer rather
than the device.

.. Warning::
    The current implementation only supports the following C data types:
    ``long``, ``double`` and ``char*`` (strings).  Thus, you can only use these
    three data types in format strings for printf, scanf and the like.

:Call: buffer = sprintf(vi, write_format, ..., buffer_length = 1024)
:VISA name: viSPrintf
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `write_format` : string
        String describing the format for arguments.
    `...` : integers, floats, or strings
        Arguments sent to the buffer according to `write_format`.
    `buffer_length` : integer : keyword argument
        Length of the user-specified buffer in bytes.  Defaults to 1024.
:Return values:
    `buffer` : string
        Buffer where the formatted data was written to.


sscanf
......

Same as `scanf`_, except that the data is read from a user-specified buffer
instead of a device.

.. Warning::
    The current implementation only supports the following C data types:
    ``long``, ``double`` and ``char*`` (strings).  Thus, you can only use these
    three data types in format strings for printf, scanf and the like.

:Call: value1, value2, ... = sscanf(vi, buffer, read_format, ...,
       maximal_string_length = 1024)
:VISA name: viSScanf
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `buffer` : string
        Buffer from which data is read and formatted.
    `read_format` : string
        String describing the format for arguments.
    `...` : integers, floats, or strings
        Arguments to be read from the device according to `read_format`.  It's
        totally insignificant which values they have, they serve just as a
        cheap way to determine what types are to be expected.  So actually this
        argument list shouldn't be necessary, but with the current
        implementation, it is, sorry.

        These arguments may be (however needn't be) the same names used for
        storing the result values.  Alternatively, you can give literals.
    `maximal_string_length` : integer : keyword argument
        The maximal length assumed for string result arguments.  Note that
        string results must *never* exceed this length.  It defaults to 1024.
:Return values:
    `value1`, `value2`, ... : integers, floats, or strings
        Arguments read from the device according to `read_format`.  Of course,
        this must be the same sequence (as far as data types are concerned) as
        the given argument list `...` above.


status_description
..................

Return a user-readable description of the status code passed to the operation.

:Call: description = status_description(vi, status)
:VISA name: viStatusDesc
:Parameters:
    `vi` : integer, ViEvent, or ViFindList
        Unique logical identifier to a session.
    `status` : integer
        Status code to interpret.
:Return values:
    `description` : string
        The user-readable string interpretation of the status code passed to
        the operation.


terminate
.........

Request a VISA session to terminate normal execution of an operation.

:Call: terminate(vi, degree, job_id)
:VISA name: viTerminate
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `degree` : integer
        ``VI_NULL``
    `job_id` : ViJobId
        Specifies an operation identifier.
:Return values:
    None.


uninstall_handler
.................

Uninstall handlers for events.

:Call: uninstall_handler(vi, event_type, handler, user_handle)
:VISA name: viUninstallHandler
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `event_type` : integer
        Logical event identifier.
    `handler` : callable
        Interpreted as a valid reference to a handler to be uninstalled by a
        client application.
    `user_handle` : ctypes type : optional
        A value specified by an application that can be used for identifying
        handlers uniquely in a session for an event.  It *must* be the object
        returned by `install_handler`_.  Consequently, it defaults to
        ``None``.
:Return values:
    None.


unlock
......

Relinquish a lock for the specified resource.

:Call: unlock(vi)
:VISA name: viUnlock
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
:Return values:
    None.


unmap_address
.............

Unmap memory space previously mapped by `map_address`_.

:Call: unmap_address(vi)
:VISA name: viUnmapAddress
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
:Return values:
    None.


unmap_trigger
.............

Undo a previous map from the specified trigger source line to the specified
destination line.

:Call: unmap_trigger(vi, trigger_source, trigger_destination)
:VISA name: viUnmapTrigger
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `trigger_source` : integer
        Source line used in previous map.
    `trigger_destination` : integer
        Destination line used in previous map.
:Return values:
    None.


usb_control_in
..............

Request arbitrary data from the USB device on the control port.

:Call: buffer = usb_control_in(vi, request_type_bitmap_field,
                   request_id, request_value, index, length)
:VISA name: viUsbControlIn
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `request_type_bitmap_field` : integer
        Bitmap field for defining the USB control port request.  The bitmap
        fields are as defined by the USB specification.  The direction bit must
        be device-to-host.
    `request_id` : integer
        Request ID for this transfer.  The meaning of this value depends on
        `request_type_bitmap_field`.
    `request_value` : integer
        Request value for this transfer.
    `index` : integer
        Specifies the interface or endpoint index number, depending on
        `request_type_bitmap_field`.
    `length` : integer : optional
        Number of data in bytes to request from the device during the Data
        stage.  If this value is not given or 0, an empty string is returned.
:Return values:
    `buffer` : string
        Actual data received from the device during the Data stage.  If
        `length` is not given or 0, an empty string is returned.


usb_control_out
...............

Send arbitrary data to the USB device on the control port.

:Call: usb_control_out(vi, request_type_bitmap_field, request_id, request_value,
                    index, buffer)
:VISA name: viUsbControlOut
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `request_type_bitmap_field` : integer
        Bitmap field for defining the USB control port request.  The bitmap
        fields are as defined by the USB specification.  The direction bit must
        be host-to-device.
    `request_id` : integer
        Request ID for this transfer.  The meaning of this value depends on
        `request_type_bitmap_field`.
    `request_value` : integer
        Request value for this transfer.
    `index` : integer
        Specifies the interface or endpoint index number, depending on
        `request_type_bitmap_field`.
    `buffer` : string : optional
        Actual data to send to the device during the Data stage.  If not given,
        nothing is sent.
:Return values:
    None.


vprintf, vqueryf, vscanf, vsprintf, vsscanf
...........................................

These variants make no sense in Python, so I realised them as mere aliases
(just drop the "v").


vxi_command_query
.................

Send the device a miscellaneous command or query and/or retrieve the response
to a previous query.

:Call: vxi_command_query(vi, mode, command)
:VISA name: viVxiCommandQuery
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `mode` : integer
        Specifies whether to issue a command and/or retrieve a response.
    `command` : integer
        The miscellaneous command to send.
:Return values:
    `response` : integer
        The response retrieved from the device.  If the mode specifies just
        sending a command, this parameter may be ``VI_NULL``.


wait_on_event
.............

Wait for an occurrence of the specified event for a given session.

:Call: out_event_type, out_context = wait_on_event(vi, in_event_type, timeout)
:VISA name: viWaitOnEvent
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `in_event_type` : integer
        Logical identifier of the event(s) to wait for.
    `timeout` : integer
        Absolute time period in milliseconds that the resource shall wait for a
        specified event to occur before returning the time elapsed error.
:Return values:
    `out_event_type` : integer
        Logical identifier of the event actually received.
    `out_context` : ViEvent
        A handle specifying the unique occurrence of an event.


write
.....

Write data to device synchronously.

:Call: return_count = write(vi, buffer)
:VISA name: viWrite
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `buffer` : string
        Contains the data block to be sent to the device.
:Return values:
    `return_count` : integer
        The number of bytes actually transferred.


write_asynchronously
....................

Write data to device asynchronously.

:Call: job_id = write_asynchronously(vi, buffer)
:VISA name: viWriteAsync
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `buffer` : string
        Contains the data block to be sent to the device.
:Return values:
    `job_id` : ViJobId
        The job identifier of this asynchronous write operation.


write_from_file
...............

Take data from a file and write it out synchronously.

:Call: return_count = write_from_file(vi, filename, count)
:VISA name: viWriteFromFile
:Parameters:
    `vi` : integer
        Unique logical identifier to a session.
    `filename` : string
        Name of file from which data will be read.
    `count` : integer
        Maximal number of bytes to be written.
:Return values:
    `return_count` : integer
        Number of bytes actually transferred.
